# Lack of Transactional Integrity

**Severity**: High

## Description

Functions that modify multiple resources without transactional integrity may leave the system in an inconsistent state
if an error occurs mid-operation.

## What Should Not Be Done

Modifying multiple resources without rollback mechanisms can lead to partial updates if an error occurs:

```rust
fn transfer_funds(sender: AccountId, recipient: AccountId, amount: u32) {
    update_balance(sender, -amount);
    update_balance(recipient, amount); // No rollback if this fails
}
```

## What Can Be Done Instead

Use atomic operations or implement rollback logic to ensure all changes are applied consistently:

```rust
fn transfer_funds(sender: AccountId, recipient: AccountId, amount: u32) -> Result<(), Error> {
    update_balance(sender, -amount)?;
    update_balance(recipient, amount)?;
    Ok(())
}
```

In this example, if any part of the operation fails, the function returns an error, ensuring data consistency.
