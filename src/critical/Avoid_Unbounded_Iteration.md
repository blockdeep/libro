# Avoid Unbounded Iterations

**Severity**: <span style="color:red;">Critical</span>

## Description

Unbounded iterations over large data structures in Substrate runtimes can lead to excessive weight consumption during transaction execution. Every operation must account for its computational cost to maintain security and prevent abuse. Unbounded iterations can result in spam or denial-of-service (DDoS) attacks if an extrinsic consumes too much weight, blocking other operations and degrading blockchain performance.

## What should be avoided

The following example illustrates an iteration over all items in `big_data_set` without any limit. In a blockchain context, such an operation can lead to unpredictable execution times and excessive resource usage:

```rust
#[pallet::storage]
pub type UnboundedData<T: Config> = StorageMap<_, Blake2_128Concat, T::AccountId, u32>;

fn iterate_over_data() {
    let big_data_set = UnboundedData::<T>::iter();
    for (acc, data) in big_data_set {
        // Process each item with no limit
    }
}
```

## Best practice

### Option 1: Process up to a maximum number of elements

Use a bounded iterator or limit the number of items processed in each iteration. This approach prevents excessive resource usage and keeps operations predictable, ensuring the execution weight remains within acceptable bounds.

```rust
const MAX_ITEMS: usize = 20;

#[pallet::storage]
pub type UnboundedData<T: Config> = StorageMap<_, Blake2_128Concat, T::AccountId, u32>;

fn iterate_over_data() {
    let big_data = UnboundedData::<T>::iter();
    for (acc, data) in big_data.take(MAX_ITEMS) {
        // Process a limited number of items safely
    }
}
```

By setting a maximum limit, you can control the processing load and avoid potential performance issues that could compromise the blockchain's stability.

### Option 2: Use a bounded data structure

Alternatively, use bounded data structures to enforce strict size limits at the data storage level. This ensures that the maximum number of iterations is predefined and controlled.

```rust
#[pallet::storage]
pub type BoundedData<T: Config> = StorageValue<_, BoundedBTreeMap<T::AccountId, u32, T::MaxEntries>>;

fn iterate_over_data() {
    let bounded_data = BoundedData::<T>::get();
    for (acc, data) in bounded_data {
        // Iterates over a data structure with bounded size.
    }
}
```

Using a bounded data structure ensures compliance with weight management policies and reduces the risk of performance bottlenecks or attacks on the blockchain.
