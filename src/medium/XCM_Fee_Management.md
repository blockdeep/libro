# XCM Fee Management

**Severity**: Medium

## Description

`FeeManager` is the most common trait implementation for handling fees charged by executors for executing XCM messages.
If set to the empty tuple, fees will be burned.

## What should be avoided

Use the `FeeManager` unit type without recognizing that this results in fee burning.

```rust
type FeeManager = ();
```

## Best Practice

Fees can be either deposited or distributed.

```rust
type FeeManager = XcmFeeManagerFromComponents<
    WaivedLocations,
    XcmFeeToAccountId20<Self::AssetTransactor, AccountId, StakingPot>,
>;
```

In this example, the `FeeManager` accepts `WaivedLocations` that are exempt from fees and transfers any charged fees to
a `StakingPot` account.
