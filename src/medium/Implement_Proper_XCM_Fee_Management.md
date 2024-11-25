# Implement Proper XCM Fee Management

**Severity**: <span style="color:gold;">Medium</span>

## Description

The `FeeManager` trait is used to manage fees for executing XCM messages. When properly configured, it allows for fees to be distributed to specified accounts or components. However, if `FeeManager` is set to the empty unit type (()), all fees will be burned

## What should be avoided

Setting FeeManager to the unit type () should be done with caution. This setting will automatically burn all fees collected.

```rust
// Fees will be burned.
type FeeManager = ();
```

## Best practice

Configure `FeeManager` to allow fees to be either deposited or distributed.

```rust
// Fees will be deposited into an account.
type FeeManager = XcmFeeManagerFromComponents<
    WaivedLocations,
    XcmFeeToAccountId20<Self::AssetTransactor, AccountId, StakingPot>,
>;
```

In this example, the `FeeManager` accepts `WaivedLocations` that are exempt from fees and transfers any charged fees to
a `StakingPot` account.
