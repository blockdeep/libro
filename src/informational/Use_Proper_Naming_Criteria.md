# Use Proper Naming Criteria

**Severity**: <span style="color:cyan;">Informational</span>

## Description

When naming terms related to assets, functions, or variables in Substrate development, it is crucial to avoid using well-known nomenclature that may already be strongly associated with other frameworks or ecosystems, such as `Asset Hub`. Misusing common terms like "foreign" or "native" can lead to confusion and misunderstandings, especially when the terminology overlaps with terms already established in other projects. It is recommended to conduct preliminary research into terms widely used by popular chains or modules to ensure clarity and consistency, preventing potential integration issues and improving the accuracy of documentation and code.

## What should be avoided

In this example, assets bridged from another consensus system are referred to as "foreign", a term strongly associated with `Asset Hub`’s foreign assets. Given the chain’s intended integration with Asset Hub, this terminology could mislead developers, potentially causing fundamental misunderstandings about the asset types referenced in the documentation.

```rust
fn transfer_foreign(receiver: T::AccountId, balance: u32) -> Result<(), Error> {
    // The name of this variable is not appropiate.
    let foreign_asset_balance: BalanceOfAsset<T> = balance.into();
    
    let pot_account: T::AccountId = Self::account_id();
    pallet_assets::Pallet::<T>::transfer_keep_alive(
        RawOrigin::Signed(pot_account.clone()).into(),
        id.clone(),
        receiver,
        foreign_asset_balance,
    )?;
    
    Ok(())
}
```

## Best practice

After conducting initial ecosystem research, particularly on chains with which the product is designed to integrate, a more informed naming decision can be made.

```rust
let bridged_asset_balance: BalanceOfAsset<T> = balance.into();
```

In this approach:

- The terminology chosen clarifies the origin and nature of the assets.
- Ambiguous terms like "native", "foreign", or "wrapped", commonly used in the context of `pallet-assets`, were avoided to prevent misunderstanding.
