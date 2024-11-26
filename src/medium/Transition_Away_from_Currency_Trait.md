# Transition Away from Currency Trait

**Severity**: <span style="color:gold;">Medium</span>

## Description

The `Currency` trait in Substrate is deprecated and should no longer be used in new implementations. Continuing to rely on deprecated traits risks compatibility issues with future framework updates and limits access to newer, more flexible features. Transitioning to the recommended traits, such as those in the `fungible` module (`Inspect`, `Mutate`, ...), ensures forward compatibility, aligns with modern development practices, and leverages the latest improvements in the Substrate ecosystem.

## What should be avoided

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

## Best practice

The usage of fungible traits is preferred instead.

```rust
// Import the traits from the fungible module
use frame_support::traits::fungible::{Inspect, Mutate};

#[pallet::config]
pub trait Config: frame_system::Config {
    // Use the preferred traits
	type Currency: Inspect<Self::AccountId> + Mutate<Self::AccountId>;
}
```
