# Break Down Complex Functions

**Severity**: <span style="color:gold;">Medium</span>

## Description

Complex functions with multiple responsibilities are harder to test, understand, and maintain, increasing the risk of errors and making debugging more difficult. In Substrate runtime development, where precise logic is critical for the correct functioning of the blockchain, overly complex functions can lead to bugs that are challenging to identify and resolve, potentially impacting the entire network.

## What should be avoided

Combining multiple responsibilities in a single function increases its complexity:

```rust
fn process_transaction() {
    // Transaction validation code
    // ...

    // Fee calculation code
    // ...

    // Balance update code
    // ...

    // Update the storage
    // ...
}
```

In this example:

- The function mixes validation, fee calculation, balance updates, and storage modifications, making it difficult to pinpoint the source of issues or extend the logic without introducing errors.

## Best practice

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
