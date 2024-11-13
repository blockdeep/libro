# Avoid Redundant Data Structures

**Severity**: <span style="color:gold;">Medium</span>

## Description

Storing the same information in multiple storage structures leads to redundancy, which increases storage complexity and
usage. Redundant storage also introduces risks of data inconsistency, as it requires additional logic to keep each
storage location synchronized, potentially causing errors or unnecessary maintenance.

## What should be avoided

Avoid creating separate data structures or fields that duplicate data already present within another structure, as this
can lead to inefficient data management.

```rust
pub struct Info<AccountId, BlockNumber> {
	pub owner: AccountId,
	pub more_data_1: u32,
	pub more_data_2: u32,
}

#[pallet::storage]
pub type SomeInfo<T: Config> =
	StorageMap<_, Identity, SomeId, Info<T::AccountId, BlockNumberFor<T>>, OptionQuery>;

#[pallet::storage]
pub type InfoOwner<T: Config> =
	StorageMap<_, Identity, SomeId, AccountId, BlockNumberFor<T>>, OptionQuery>;
```

In this example:

- The `InfoOwner` storage map is redundant since the owner is already stored within the `Info` structure that is part of the `SomeInfo` StorageMap.

## Best practice

To prevent redundant storage usage, maintain data within a single structure or storage map whenever possible. If data
needs to be accessed frequently, consider optimizing retrieval methods rather than duplicating data in multiple places.

```rust
pub struct Info<AccountId, BlockNumber> {
	pub owner: AccountId,
	pub more_data_1: u32,
	pub more_data_2: u32,
}

#[pallet::storage]
pub type SomeInfo<T: Config> =
	StorageMap<_, Identity, SomeId, Info<T::AccountId, BlockNumberFor<T>>, OptionQuery>;
```

In this example:

- The `InfoOwner` storage map was deleted to remove storage redundancy.
