# Expose Runtime APIs for Key Functionalities

**Severity**: <span style="color:green;">Low</span>

## Description

Runtime APIs in Substrate are a vital mechanism for exposing key runtime functionalities to external clients, such as frontend applications, wallets, or other off-chain systems. These APIs provide a way for external parties to interact with the blockchain, query on-chain data, and invoke runtime logic remotely, all while maintaining the security and integrity of the blockchain.

Failing to expose essential functions via Runtime APIs limits access to valuable runtime data, preventing users and clients from retrieving crucial on-chain information or interacting with the blockchain efficiently. By exposing necessary runtime functionalities, developers can enable richer, more interactive decentralized applications (dApps), fostering a more connected ecosystem.

## What should be avoided

Avoid limiting key functionalities to internal runtime use only, as shown below:

```rust
// Functionality only accessible inside the pallet.
pub fn pot_account() -> T::AccountId {
	T::PotId::get().into_account_truncating()
}
```

In this example:

- Although a function is available to retrieve the account ID of an internal pot, it is only accessible within the runtime. This limitation prevents clients or users from querying the account balance or initiating transfers to this account, as there is no way to know which account this is.

## Best practice

Expose necessary runtime functionalities by implementing Runtime APIs. This approach allows external users or clients to access useful information as needed.

```rust
// pallet/lib.rs
sp_api::decl_runtime_apis! {
	/// This runtime api allows to query the pot account.
	pub trait PalletApi<AccountId>
	where
		AccountId: Codec,
	{
		/// Queries the pot account.
		fn pot_account() -> AccountId;
	}
}

// runtime/lib.rs
impl pallet::PalletApi<Block, AccountId> for Runtime {
	pub fn pot_account() -> AccountId {
		Pallet::pot_account()
	}
}
```
