# Lack of Transactional Integrity

**Severity**: High

## Description

Functions that modify multiple resources without transactional integrity may leave the system in an inconsistent state
if an error occurs mid-operation.

## What should not be done

Modifying multiple resources without rollback mechanisms can lead to partial updates if an error occurs:

```rust
fn transfer_funds(sender: &AccountId, recipient: &AccountId, amount: u32) {
    reduce_balance(sender, amount);
    
    // No rollback if this fails
    increase_balance(recipient, amount);
}
```

## What can be done instead

Use atomic operations or implement rollback logic to ensure all changes are applied consistently:

```rust
fn transfer_funds(sender: &AccountId, recipient: &AccountId, amount: u32) -> Result<(), Error> {
    reduce_balance(sender, amount)?;
    increase_balance(recipient, amount)?;
    Ok(())
}
```

In this example, if any part of the operation fails, the function returns an error, ensuring data consistency.
