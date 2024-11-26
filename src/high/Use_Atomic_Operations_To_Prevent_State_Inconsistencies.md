# Use Atomic Operations to Prevent State Inconsistencies

**Severity**: High

## Description

Functions that modify multiple resources without transactional integrity may leave the system in an inconsistent state if an error occurs mid-operation. In a blockchain environment, where state consistency is critical to maintain trust and operational stability, this can lead to data corruption, incorrect balances, or unexpected behavior.

## What should be avoided

Modifying multiple resources without rollback mechanisms can lead to partial updates if an error occurs:

```rust
fn transfer_funds(sender: &T::AccountId, recipient: &T::AccountId, amount: u32) {
    reduce_balance(sender, amount);

    // Ignoring the result. No rollback if this fails.
    let _ = increase_balance(recipient, amount);
}
```

In this example:

- **Lack of Error Handling**: If `increase_balance` fails, there is no mechanism to revert the changes made by `reduce_balance`. This results in an inconsistent state where the sender’s balance is reduced, but the recipient’s balance remains unchanged, violating the atomicity of the transaction.

## Best practice

Use atomic operations or implement rollback logic to ensure all changes are applied consistently:

```rust
// Add the Result<(), Error> return type to allow a
// rollback if an error occurs in any of the functions.
fn transfer_funds(sender: &T::AccountId, recipient: &T::AccountId, amount: u32) -> Result<(), Error> {
    reduce_balance(sender, amount)?;
    increase_balance(recipient, amount)?;
    Ok(())
}
```

In this example:

- **Transactional Integrity**: If any part of the operation fails, the function returns an error, and no changes are committed.
- **Consistency**: Both `reduce_balance` and `increase_balance` succeed or fail together, maintaining the state integrity of the system.

Ensuring atomicity in such operations prevents inconsistencies and safeguards the reliability of the blockchain state.
