# Handle Storage Growth

**Severity**: High

## Description

Allowing unlimited entries in storage structures can lead to overflow, increased costs, and performance issues during
operations that manage these entries.

## What should be avoided

The following code allows adding entries without any limit, leading to uncontrolled storage growth:

```rust
#[pallet::storage]
pub type Entries<T: Config> = StorageValue<_, Vec<Entry>>;

fn add_entry(entry: Entry) {
    // Adds entries without limits
    entries.push(entry);
}
```

## Best Practice

Using `BoundedVec`, we can set a fixed maximum number of entries, enforcing storage limits directly within the data
structure. This approach automatically restricts the growth of entries, enhancing efficiency.

```rust
#[pallet::storage]
pub type Entries<T: Config> = StorageValue<_, BoundedVec<Entry, T::MaxEntries>>;

fn add_entry_limited(entry: Entry) -> Result<(), Error> {
    Entries::<T>::try_push(entry).map_err(|_| Error::<T>::TooManyEntries)
}
```

Here, the `BoundedVec` ensures that the number of entries cannot exceed `T::MaxEntries`, which enforces storage limits
directly. This approach maintains predictable storage usage and efficient operations by preventing uncontrolled
accumulation of data.
