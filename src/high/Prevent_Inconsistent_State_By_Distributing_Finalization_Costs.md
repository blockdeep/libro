# Prevent Inconsistent State by Distributing State Commitment Costs

**Severity**: <span style="color:orange;">High</span>

## Description

Relying on a blanket extrinsic to commit multiple storage entities or operations can lead to excessive costs, penalties, or errors, especially if the transaction fails. This approach risks incomplete operations and could lead to inconsistent state. In blockchain systems, atomicity is critical; partial updates or failures during state commitments can compromise system integrity and lead to unintentional bugs or vulnerabilities.

## What should be avoided

In the following example, one function is responsible for committing all previous mutations, leading to a single point of failure and high resource usage:

```rust
#[pallet::storage]
pub type PendingOperations<T: Config> = StorageValue<_, Vec<UserOperation>>;

fn finalize_operations() {
    let pending_operations = PendingOperations::<T>::get();
    for operation in pending_operations {
        // Committing all items at once
        complete_operation(operations);
        commit_storage([users]);
        mutate_items([other_items]);
    }
}
```

Using this method:
- A failure in processing any item could result in none of the operations being applied.
- Attempting to commit all operations at once increases the execution weight, making it more likely to exceed block limits or cause out-of-gas errors.

## Best practice

Use a claim-based approach where each user commits their operation individually, or use batch processing to distribute the load.

```rust
fn claim_operation(participant: T::AccountId) -> Result<(), Error> {
    // Each participant commits their own operation
    complete_operation_for(participant)?;
    Ok(())
}
```

This approach spreads finalization costs across participants, reducing the risk of a single transaction failing and making the system more scalable and resilient. By isolating operations to individual participants or smaller groups, the state remains consistent, and the system can handle larger workloads without risking failure.
