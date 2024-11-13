# Implement Proper XCM Fee Management

**Severity**: <span style="color:gold;">Medium</span>

## Description

The `FeeManager` trait is used to manage fees for executing XCM messages. When properly configured, it allows for fees to be distributed to specified accounts or components. However, if `FeeManager` is set to the empty unit type (()), all fees will be burned

## What should be avoided

Setting FeeManager to the unit type () should be done with caution. This setting will automatically burn all fees collected.

```rust
type FeeManager = (); // Fees will be burned
```

## Best practice

Configure `FeeManager` to allow fees to be either deposited or distributed.

```rust
type FeeManager = XcmFeeManagerFromComponents<
    WaivedLocations,
    XcmFeeToAccountId20<Self::AssetTransactor, AccountId, StakingPot>,
>;
```

In this example, the `FeeManager` accepts `WaivedLocations` that are exempt from fees and transfers any charged fees to
a `StakingPot` account.
