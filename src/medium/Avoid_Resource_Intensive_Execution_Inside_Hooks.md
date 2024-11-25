# Avoid Resource Intensive Execution Inside Hooks

**Severity**: <span style="color:gold;">Medium</span>

## Description

Performing resource-intensive operations, such as iterating over large data sets, within runtime hooks like
`on_finalize` can significantly impact block execution time and lead to performance bottlenecks. Hooks are triggered
automatically for every block, and if they contain complex or large-scale computations, there could be a reduction in
transaction throughput and potentially affect the network’s overall performance.

## What should be avoided

Avoid conducting heavy computations or iterating through extensive data in hooks, as this adds unnecessary workload to
every block. For example, consider the following inefficient approach in `on_finalize`, which processes votes for each
proposal that ends within a block:

```rust
impl<T: Config> Hooks<BlockNumberFor<T>> for Pallet<T> {
    fn on_finalize(block_number: T::BlockNumber) {
        // Retrieve proposals that have ended at this block number
        let proposals = EndedProposals::<T>::get(block_number);

        for proposal_id in proposals {
            let mut ayes = 0;
            let mut nays = 0;

            // Retrieve all votes for the current proposal
            let votes = Votes::<T>::get(proposal_id);

            for vote in votes {
                match vote {
                    VoteType::Aye => ayes = ayes.saturating_add(1),
                    VoteType::Nay => nays = nays.saturating_add(1)
                }
            }

            // Process `ayes` and `nays` results as needed
        }
    }
}
```

In this example:

- Counting votes for each finalized proposal during `on_finalize` leads to high resource usage and may exceed block
  weight limits, especially as the number of proposals and votes grows.

## Best practice

Optimize by performing the calculations within the extrinsics, maintaining incremental counters in storage, or enabling
users to trigger the logic explicitly outside the hooks.

### Option 1: Perform the execution within the extrinsic

Track necessary values as they are submitted, distributing the computation workload across each transaction.

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::some_vote())]
pub fn some_vote(
    origin: OriginFor<T>,
	vote: VoteType
) -> DispatchResult {
    // Any verification logic
    // ...
    ProposalVoteAmount::<T>::mutate(id, |item| -> Result<(), Error> {
        match vote {
            VoteType::Aye => *item.ayes = item.ayes.saturating_add(1),
            VoteType::Nay => *item.nays = item.nays.saturating_add(1);
        }
    })
}

fn on_finalize(block_number: T::BlockNumber) {
    // Retrieve proposals that have ended at this block number
    let proposals = EndedProposals::<T>::get(block_number);

    for proposal_id in proposals {
        let (ayes, nays) = ProposalVoteAmount::<T>::get(proposal_id);
        // Process `ayes` and `nays` results as needed
    }
}
```

### Option 2: Allow users to trigger the logic explicitly

Allow users to close/finalize manually by explicitly calling an extrinsic when necessary, which avoids performing the
work automatically in `on_finalize`.

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::close_proposal())]
pub fn close_proposal(
    origin: OriginFor<T>,
	proposal_id: ProposalId
) -> DispatchResult {
    // previous logic
    // ...

    let proposal = Proposals::<T>::get(proposal_id);
    // Make sure proposal has not ended
    ensure!(proposal.end_block < current_block, Error::<T>::ProposalHasNotEnded);

    // Proceed to calculation
    let mut ayes = 0;
    let mut nays = 0;

    // Retrieve all votes for the current proposal
    let votes = Votes::<T>::get(proposal_id);

    for vote in votes.iter() {
        match vote {
            VoteType::Aye => ayes = ayes.saturating_add(1),
            VoteType::Nay => nays = nays.saturating_add(1)
        }
    }

    // Process `ayes` and `nays` results as needed
}
```
