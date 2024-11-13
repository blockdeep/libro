# Avoid Unbounded Iterations

**Severity**: Critical

## Description

Unbounded iterations over large data structures can lead to resource exhaustion and may result in denial of service (
DoS) attacks if the process consumes too many resources.

## What should be avoided

The following code iterates over all items in `big_data` without any limit, which can overwhelm system resources if
`big_data` is large:

```rust
for item in big_data {
    // Process each item with no limit
}
```

## Best practice

### Option 1: Process up to a maximum number of elements

Use a bounded iterator or limit the number of items processed in each iteration. This approach prevents excessive
resource usage and keeps operations predictable.

```rust
for item in big_data.iter().take(MAX_ITEMS) {
    // Process a limited number of items safely
}
```

By setting a maximum limit, we can control the processing load and avoid potential performance issues.

### Option 2: Use a bounded data structure

Alternatively, you can use bounded data structures and perform the iteration over them.

```rust
#[pallet::storage]
pub type BoundedData<T: Config> = StorageValue<_, BoundedVec<u32, T::MaxEntries>>;

for item in BoundedData::<T>::get() {
    // Iterates over a data structure with bounded size.
}
```

By using a bounded data structure, we ensure the maximum number of iterations is under control.
