# Excessive Function Complexity

**Severity**: Medium

## Description

Complex functions with multiple responsibilities are harder to test, understand, and maintain, increasing the risk of
errors and making debugging more difficult.

## What Should Not Be Done

Combining multiple responsibilities in a single function increases its complexity:

```rust
fn process_transaction() {
    // Transaction validion code
    // ...
    
    // Fee calculation code
    // ...
    
    // Balance update code
    // ...
    
    // Update the storage
    // ...
}
```

## What Can Be Done Instead

Apply the single responsibility principle by breaking down the function into smaller, focused functions:

```rust
fn process_transaction() {
    validate_transaction();
    apply_fees();
    update_balances();
    record_transaction();
}
```

This approach simplifies each function, making it easier to test and understand.