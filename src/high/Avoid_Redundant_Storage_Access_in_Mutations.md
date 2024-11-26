# Avoid Redundant Storage Access in Mutations

**Severity**: <span style="color:orange;">High</span>

## Description

In Substrate runtime development, improper usage of `try_mutate` can lead to redundant storage operations, negatively impacting performance and increasing the overall weight of the extrinsic. Using both `try_mutate` and `insert` in the same closure causes unnecessary overhead by performing multiple storage accesses, which is particularly costly in terms of computation and I/O in a blockchain environment.

## What should be avoided

Using `try_mutate` followed by `insert` in a nested closure results in redundant writes:

```rust
#[pallet::storage]
pub type MyStorage<T: Config> = StorageValue<_, u32>;

let new_value = 4_u32;
MyStorage::<T>::try_mutate(id, |item| -> Result<(), Error> {
    // Raise an error if the condition is not met
    ensure!(new_value < 10 && item.is_none(), Error::<T>::InvalidValue);
    
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
