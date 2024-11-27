# Avoid Repetitive Generic Type Instantiation

**Severity**: <span style="color:green;">Low</span>

## Description

Repeatedly defining complex generic types in Substrate can make the code unnecessarily verbose and harder to maintain. When a specific instance of a generic type is needed multiple times, repeating its definition can clutter the code, increase the risk of errors, and make it more challenging to update the type when changes are required. By using type aliases for complex generic types, developers can simplify the code, improve readability, and make it easier to maintain by ensuring that the type is only defined once.

## What should be avoided

Avoid duplicating the entire definition of a complex type instance across multiple places in the code.

```rust
pub struct SomeInfo<BoundedNameString, BoundedDescString, InfoType, StatusType, AccountId, BlockNumber, MaxReasonLength> {
    pub name: BoundedNameString,
    pub description: BoundedDescString,
    pub info_type: InfoType,
    pub status: StatusType,
    pub created_by: AccountId,
    pub created_at: BlockNumber,
    pub result: Result,
    pub reason: MaxReasonLength,
}

#[pallet::storage]
pub type InfoStorage<T: Config> = StorageMap<
    _,
    Blake2_128Concat,
    T::SomeId,
    SomeInfo<
        BoundedVec<u8, T::MaxNameLength>,
        BoundedVec<u8, T::MaxDescLength>,
        T::Info,
        T::Status,
        T::AccountId,
        BlockNumberFor<T>,
        BoundedVec<u8, T::MaxReasonLength>
    >,
    ValueQuery
>;

pub fn do_something(
    origin: OriginFor<T>,
    info: SomeInfo<
        BoundedVec<u8, T::MaxNameLength>,
        BoundedVec<u8, T::MaxDescLength>,
        T::Info,
        T::Status,
        T::AccountId,
        BlockNumberFor<T>,
        BoundedVec<u8, T::MaxReasonLength>
    >
) -> DispatchResult { /* Rest of the logic */ }
```

In this example:

- The `SomeInfo` generic type is defined twice with the same parameters, making the code repetitive and harder to maintain.

## Best practice

Define a type alias for the specific instance of the generic type, and reuse this alias throughout the code. By creating a single type alias, such as `SomeInfoOf<T>`, for the specific instance, you can reference it without repeating its full definition.

```rust
pub type SomeInfoOf<T> = SomeInfo<
    BoundedVec<u8, T::MaxNameLength>,
    BoundedVec<u8, T::MaxDescLength>,
    T::Info,
    T::Status,
    T::AccountId,
    BlockNumberFor<T>,
    BoundedVec<u8, T::MaxReasonLength>
>

#[pallet::storage]
pub type InfoStorage<T: Config> = StorageMap<_, Blake2_128Concat, T::SomeId, SomeInfoOf<T>, ValueQuery>;

pub fn do_something(
    origin: OriginFor<T>,
    info: SomeInfoOf<T>
) -> DispatchResult { /* Rest of the logic */ }
```
