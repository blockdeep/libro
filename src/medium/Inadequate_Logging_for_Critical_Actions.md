# Inadequate Logging for Critical Actions

**Severity**: Medium

## Description

Failing to log critical actions can make it difficult to trace and debug issues, especially when tracking user actions
or system changes.

## What should not be done

Omitting logging for important events makes it hard to identify what happened if an issue arises:

```rust
fn update_user_balance(user_id: u32, amount: u32) {
    // Updates user balance without logging
    balances.insert(user_id, amount);
}
```

## What can be done instead

Add detailed logging for critical actions to improve traceability:

```rust
fn update_user_balance(user_id: u32, amount: u32) {
    log::info!("Updating balance for user: {}, new amount: {}", user_id, amount);
    balances.insert(user_id, amount);
}
```

This approach ensures that key actions are recorded, aiding in debugging and providing an audit trail for critical
changes.
