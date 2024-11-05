# Hardcoded `BoundedVec` Size

**Severity**: Medium

## Description

The use of a hardcoded size for `BondedVec` limits flexibility and maintainability. Introducing a configurable parameter
allows for easier adjustments and improves readability and code scalability.

## What should not be done

Using a fixed size for `BondedVec` without a configurable option restricts adaptability:

```rust
// Hardcoded size

#[pallet::storage]
pub type Domain = BondedVec<u8, ConstU32<256>>;
```

## What can be done instead

Define the size as a configurable parameter within the `Config` trait, which provides flexibility for future changes:

```rust
#[pallet::config]
pub trait Config: frame_system::Config {
    type MaxDomainSize: Get<u32>;
}

#[pallet::storage]
pub type Domain<T> = BoundedVec<u8, T::MaxDomainSize>;
```

This approach allows the `MaxDomainSize` to be defined in the runtime configuration, making the code adaptable and
easier to maintain.
