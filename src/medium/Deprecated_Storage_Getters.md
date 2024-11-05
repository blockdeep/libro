# Deprecated Storage Getters

**Severity**: Medium

## Description

The `#[pallet::getter]` attribute in Substrate is deprecated and may lead to compatibility issues in future framework
versions. Using direct access methods or new approaches for storage access helps maintain compatibility and aligns with
current best practices.

## What should not be done

Using `#[pallet::getter]` to define storage getters can lead to issues with future updates, as shown below:

```rust
#[pallet::storage]
#[pallet::getter(fn deprecated_getter)]
pub type MyValue<T> = StorageValue<_, u32>;
```

In this example:

- The `#[pallet::getter]` attribute defines a deprecated getter function (`deprecated_getter`), which may no longer be
  supported in future Substrate versions.

## What can be done instead

Access the storage value directly or use custom functions to handle storage access without relying on deprecated
getters:

```rust
#[pallet::storage]
pub type MyValue<T> = StorageValue<_, u32>;

pub fn get_my_value() -> Option<u32> {
    MyValue::<T>::get()
}
```

In this example:

- The `get_my_value` function provides controlled access to the storage item without using `#[pallet::getter]`,
  maintaining compatibility with future updates.
- This approach ensures that storage access remains up-to-date and adaptable to evolving framework standards.
