# Avoid Redundant Data Structures

**Severity**: <span style="color:gold;">Medium</span>

## Description

Storing the same information in multiple storage structures leads to redundancy, which increases storage complexity and usage. In Substrate runtimes, where every storage access contributes to execution weight, redundant storage not only wastes resources but also introduces risks of data inconsistency. Synchronizing multiple storage locations adds unnecessary complexity to the logic and increases the likelihood of errors, making maintenance more challenging.

## What should be avoided

Avoid creating separate data structures or fields that duplicate data already present within another structure, as this can lead to inefficient data management.

```rust
pub struct Info<AccountId, BlockNumber> {
	pub owner: AccountId,
	pub valid_until: BlockNumber,
	pub more_data_1: u32,
	pub more_data_2: u32,
}

#[pallet::storage]
pub type SomeInfo<T: Config> =
	StorageMap<_, Blake2_128Concat, SomeId, Info<T::AccountId, BlockNumberFor<T>>, OptionQuery>;

#[pallet::storage]
pub type InfoOwner<T: Config> = StorageMap<_, Blake2_128Concat, SomeId, T::AccountId, OptionQuery>;
```

In this example:

- The `InfoOwner` storage map is redundant since the owner is already stored within the `Info` structure that is part of the `SomeInfo` storage map.

## Best practice

To prevent redundant storage usage, maintain data within a single structure or storage map whenever possible. If data needs to be accessed frequently, consider optimizing retrieval methods rather than duplicating data in multiple places.

```rust
pub struct Info<AccountId, BlockNumber> {
	pub owner: AccountId,
	pub valid_until: BlockNumber,
	pub more_data_1: u32,
	pub more_data_2: u32,
}

#[pallet::storage]
pub type SomeInfo<T: Config> =
	StorageMap<_, Blake2_128Concat, SomeId, Info<T::AccountId, BlockNumberFor<T>>, OptionQuery>;
```

In this example:

- The `InfoOwner` storage map was deleted to remove storage redundancy. Retrieval of the `owner` field can now be performed directly from the `Info` structure within `SomeInfo`, ensuring consistency and reducing maintenance complexity.
