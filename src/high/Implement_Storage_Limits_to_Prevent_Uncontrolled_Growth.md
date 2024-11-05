# Implement Storage Limits to Prevent Uncontrolled Growth

**Severity**: High

## Description

Allowing unlimited entries in storage structures can lead to overflow, increased costs, and performance issues during
operations that manage these entries.

## What should not be done

The following code allows adding entries without any limit, leading to uncontrolled storage growth:

```rust
fn add_entry(entry: Entry) {
    // Adds entries without limits
    entries.push(entry);
}
```

## What can be done instead

Using `BoundedVec`, we can set a fixed maximum number of entries, enforcing storage limits directly within the data
structure. This approach automatically restricts the growth of entries, enhancing efficiency.

```rust
#[pallet::storage]
pub type Entries<T: Config> = StorageValue<_, BoundedVec<Entry, MaxEntries>>;

fn add_entry_limited(entry: Entry) -> Result<(), &'static str> {
    Entries::<T>::try_push(entry).map_err(|_| "Max entries limit reached")
}
```

Here, the `BoundedVec` ensures that the number of entries cannot exceed `MaxEntries`, which enforces storage limits
directly. This approach maintains predictable storage usage and efficient operations by preventing uncontrolled
accumulation of data.
