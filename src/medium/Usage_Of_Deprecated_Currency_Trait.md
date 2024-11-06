# Usage of deprecated Currency trait

**Severity**: Medium

## Description

Using deprecated traits, such as `Currency`, can lead to issues with compatibility in newer versions of Substrate and
may limit functionality as updates to the ecosystem continue. Migrating to the recommended traits ensures ongoing
support, compatibility with future releases, and access to newer features.

## What should not be done

Avoid using the deprecated `Currency` trait in new implementations:

```rust
use frame_support::traits::Currency;

#[pallet::config]
pub trait Config: frame_system::Config {
    // Currency trait is deprecated
    type Currency: Currency<Self::AccountId>;
}
```

In this example:

- The `Currency` trait is used to handle account balances. This trait is already deprecated and should not be used.

## What can be done instead

The usage of fungible traits is preferred instead.

```rust
use frame_support::traits::{Inspect, Mutate};

#[pallet::config]
pub trait Config: frame_system::Config {
	type Currency: Inspect<Self::AccountId> + Mutate<Self::AccountId>;
}
```
