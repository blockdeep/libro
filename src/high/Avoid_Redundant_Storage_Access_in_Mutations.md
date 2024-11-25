# Avoid Redundant Storage Access in Mutations

**Severity**: <span style="color:orange;">High</span>

## Description

Improper usage of `try_mutate` leads to redundant storage operations, which can negatively impact performance. Using both `try_mutate` and `insert` in the same closure causes unnecessary overhead by performing multiple accesses to storage.

## What should be avoided

Using `try_mutate` followed by `insert` in a nested closure causes redundant writes:

```rust
#[pallet::storage]
pub type MyStorage<T: Config> = StorageValue<_, u32>;

let new_value = 4_u32;
MyStorage::<T>::try_mutate(id, |item| -> Result<(), Error> {
    // Raise an error if the condition is not met
    ensure!(new_value < 10, Error::<T>::InvalidValue);
    
    *item = Some(new_value);

    // Redundant insert
    MyStorage::<T>::insert(id, new_value);

    Ok(())
})?;
```

## Best practice

Use either `try_mutate` to modify the value in place or `insert` alone, but avoid combining them unnecessarily:

```rust
#[pallet::storage]
pub type MyStorage<T: Config> = StorageValue<_, u32>;

let new_value = 4_u32;
MyStorage::<T>::try_mutate(id, |item| -> Result<(), Error> {
    // Raise an error if the condition is not met
    ensure!(new_value < 10, Error::<T>::InvalidValue);
    
    *item = Some(new_value);
    Ok(())
})?;
```

This approach reduces storage accesses, improving both performance and resource efficiency.
