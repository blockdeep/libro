# Ensure Consistent Asset Registration by Adhering to Host Chain Schema

**Severity**: <span style="color:orange;">High</span>

## Description

Asset representation on other chains must be carefully studied before registering the asset(s) on your chain, as XCMP and `pallet-assets` do not necessarily limit the possible `AssetId` assignments. This flexibility could result in registering an asset under a different schema than that used by other users or proposed by the host chain, potentially leading to serious integration issues.

## What should be avoided

Consider a system that uses a `Location` schema to represent both local and foreign assets — i.e., assets originating from other consensus systems.

In this system, native assets from other chains are represented by their `Location`. Assuming the host chain and Chain X are both connected to the same `Relay`, the native asset of Chain X would be represented as:

```rust
// In runtime/xcm_config.rs file
pub const AssetOfX: Location = Location::new(1, [Parachain(PARA_ID_OF_X)]);
```

Now, suppose Chain Y integrates with the host system and registers its native asset as follows:

```rust
// In runtime/xcm_config.rs file
pub const AssetOfY: Location = Location::new(1, [Parachain(PARA_ID_OF_Y), GeneralIndex(0)]);
```

While this could be accepted by the host system, it disrupts the established schema. For example, front-ends integrated with the host would now need to account for an additional `Junction` to retrieve `ASSET_OF_Y`, creating an exception that complicates integration and consistency across assets.

## Best practice

The host’s adopted schema must be carefully studied and followed. In the case of `AssetOfY`, it should be registered as follows:

```rust
// In runtime/xcm_config.rs file
pub const AssetOfY: Location = Location::new(1, [Parachain(PARA_ID_OF_Y)]);
```

More complex cases, such as `pallet-assets`' created assets from another system, may have a more intricate `Location`. Nonetheless, the host should provide a clear schema, which all integrating systems are expected to respect and adhere to.
