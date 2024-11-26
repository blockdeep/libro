# Include Extrinsic Documentation

**Severity**: <span style="color:gold;">Medium</span>

## Description

An extrinsic in Substrate is a primary interface for interacting with the blockchain. It represents a transaction or an inherent operation submitted by users or the system itself, allowing them to invoke specific logic defined in the runtime. As extrinsics directly impact the state of the blockchain, ensuring their functionality, clarity, and correctness is crucial for maintaining the network's integrity. Proper documentation of extrinsics provides developers and users with the context needed to understand their purpose, inputs, permissions, and potential outcomes, reducing the risk of misuse or errors.

A lack of documentation for extrinsics can lead to confusion about their functionality, expected inputs, permissions, and possible errors. This makes it harder for developers and users to correctly interact with the runtime. Providing comprehensive documentation for extrinsics ensures clarity, improves usability, and offers valuable insights to both frontend clients and users, reducing the likelihood of misuse or unexpected errors.

## What should be avoided

Leaving extrinsics undocumented makes it difficult to understand their behavior, which may lead to misuse or unexpected
errors:

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::transfer())]
pub fn transfer(sender: OriginFor<T>, recipient: AccountId, amount: BalanceOf<T>) {
    // Performs operation with no explanation of parameters, permissions, or errors
}
```

## Best practice

Document each extrinsic clearly, detailing its purpose, input parameters, permissions, and potential errors to improve
usability and clarity:

```rust
/// Transfers a specified amount from the sender to the recipient.
///
/// # Parameters
/// - `sender`: The origin initiating the transfer.
/// - `recipient`: The account ID of the entity receiving the funds.
/// - `amount`: The amount to be transferred.
///
/// # Permissions
/// Only callable by accounts with sufficient balance to cover the `amount`.
///
/// # Errors
/// - `InsufficientBalance` if the sender's balance is too low.
/// - `InvalidRecipient` if the recipient account is invalid.
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::transfer())]
pub fn transfer(sender: OriginFor<T>, recipient: AccountId, amount: BalanceOf<T>) -> DispatchResult {
    // Function implementation here
}
```

In this example:

- Each parameter, required permission, and potential error is clearly documented, ensuring users know exactly how to interact with the extrinsic and what conditions to expect.
- This level of detail minimizes confusion and supports safer, more effective use of the extrinsic.
