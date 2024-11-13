# Use Proper Naming Criteria

**Severity**: Informational

## Description

It is recommended to avoid using well-known nomenclature for naming conventions. Conduct preliminary research on terms
commonly used by popular chains (e.g., relay chains or system chains) before finalizing names.

## What should be avoided

In this example, assets bridged from another consensus system are referred to as "foreign", a term strongly associated
with `Asset Hub`’s foreign assets. Given the chain’s intended integration with Asset Hub, this terminology could mislead
developers, potentially causing fundamental misunderstandings about the asset types referenced in the documentation.

```rust
let foreign_asset_balance: BalanceOfAsset<T> = balance.into();

let pot_account = Self::account_id();

pallet_assets::Pallet::<T>::transfer_keep_alive(
    RawOrigin::Signed(pot_account.clone()).into(),
    id.clone(),
    T::Lookup::unlookup(who.clone()),
    foreign_asset_balance,
)?;
```

## Best practice

After conducting initial ecosystem research, particularly on chains with which the product is designed to integrate, a
more informed naming decision can be made.

```rust
let bridged_asset_balance: BalanceOfAsset<T> = balance.into();
```

In this approach:

- The terminology chosen clarifies the origin and nature of the assets.
- Ambiguous terms like "native", "foreign", or "wrapped", commonly used in the context of `pallet-assets`, were avoided
  to prevent misunderstanding.
