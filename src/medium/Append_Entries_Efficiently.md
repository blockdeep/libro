# Append Entries Efficiently

**Severity**: <span style="color:gold;">Medium</span>

## Description

Using `try_append` instead of `try_mutate` for a Substrate `StorageValue` has several advantages. Specifically,
`try_append` is more efficient because it avoids reading and rewriting the entire storage value, resulting in lower
computation and storage costs when appending a single item. This makes it particularly useful for operations where the
goal is simply to append an entry without other modifications. By contrast, `try_mutate` reads the entire storage value
into memory, modifies it, and writes it back, which can be both computationally and storage-intensive for large
collections.

## What should be avoided

Using `try_mutate` has a severe penalty when compared to `try_append` and should be avoided whenever possible.

```rust
#[pallet::storage]
pub type Entries<T: Config> = StorageValue<_, BoundedVec<u32, T::MaxEntries>>;

#[pallet::error]
pub enum Error<T> {
	/// MaxEntries limit reached.
	TooManyEntries,
}

fn add_entry(entry: u32) -> Result<(), DispatchError> {
    // Adds a new entry by reading the whole storage item and editing it. This is inefficient.
    Entries::<T>::try_mutate(|entries| {
        entries.try_push(entry).map_err(|_| Error::<T>::TooManyEntries)?;
        Ok(())
    })
}
```

## Best practice

Use `try_append` for improved readability and efficiency.

```rust
fn add_entry(entry: u32) -> Result<(), DispatchError> {
    // Adds a new entry efficiently.
    Entries::<T>::try_append(entry).map_err(|_| Error::<T>::TooManyEntries)?;
    Ok(())
}
```

