# Usage of deprecated Currency trait

**Severity**: Medium

## Description

Using deprecated traits, such as Currency, can lead to issues with compatibility in newer versions of Substrate and may limit functionality as updates to the ecosystem continue. Migrating to the recommended traits ensures ongoing support, compatibility with future releases, and access to newer features.

## What should not be done

Avoid using the deprecated `Currency` trait in new implementations

```rust
#[pallet::config]
pub trait Config: frame_system::Config {
    type RuntimeEvent: From<Event<Self>> + IsType<<Self as frame_system::Config>::RuntimeEvent>;
    ...
    type Currency: Currency<Self::AccountId>;  //Currency trait is deprecated
}
```

In this example:

- The Currency trait is used to handle account balances. This trait is already deprecated and should not be used.

## What can be done instead

The usage of fungible traits is prefered instead.

```rust
#[pallet::config]
pub trait Config: frame_system::Config {
    type RuntimeEvent: From<Event<Self>> + IsType<<Self as frame_system::Config>::RuntimeEvent>;
    ...
	type Currency: fungible::Inspect<Self::AccountId>
			+ fungible::Mutate<Self::AccountId>
}
```
