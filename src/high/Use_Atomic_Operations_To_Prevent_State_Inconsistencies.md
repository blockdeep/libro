# Use Atomic Operations to Prevent State Inconsistencies

**Severity**: High

## Description

Functions that modify multiple resources without transactional integrity may leave the system in an inconsistent state
if an error occurs mid-operation.

## What should be avoided

Modifying multiple resources without rollback mechanisms can lead to partial updates if an error occurs:

```rust
fn transfer_funds(sender: &AccountId, recipient: &AccountId, amount: u32) -> () {
    reduce_balance(sender, amount);

    // No rollback if this fails
    increase_balance(recipient, amount);
}
```

In this example:

- Lack of Error Handling: If increase_balance fails, there is no mechanism to revert the changes made by reduce_balance. This creates an inconsistent state where the sender’s balance has been reduced, but the recipient’s balance hasn’t been updated accordingly, leading to potential issues in the system’s data integrity.

## Best Practice

Use atomic operations or implement rollback logic to ensure all changes are applied consistently:

```rust
// Add the Result<(), Error> return type to allow a
// rollback if an error occurs in any of the funtions
fn transfer_funds(sender: &AccountId, recipient: &AccountId, amount: u32) -> Result<(), Error> {
    reduce_balance(sender, amount)?;
    increase_balance(recipient, amount)?;
    Ok(())
}
```

In this example, if any part of the operation fails, the function returns an error, ensuring data consistency.
