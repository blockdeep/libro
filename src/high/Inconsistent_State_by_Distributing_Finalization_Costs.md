# Prevent Inconsistent State by Distributing Finalization Costs

**Severity**: High

## Description

Relying on a single transaction to finalize multiple operations can lead to excessive costs, penalties, or errors,
especially if the final transaction fails. This approach risks incomplete operations and impacts system reliability.

## What should not be done

In the following example, one function is responsible for finalizing all previous actions, leading to a single point of
potential failure and high resource usage:

```rust
fn finalize_operations() {
    for item in pending_operations {
        // Finalizing all operations at once
        complete_operation(item);
    }
}
```

## What can be done instead

Use a claim-based process where each participant finalizes their operation individually, or use batch processing to
distribute the load.

```rust
fn claim_operation(participant: AccountId) -> Result<(), Error> {
    // Each participant finalizes their own operation
    complete_operation_for(participant)?;
    Ok(())
}
```

This approach spreads finalization costs across participants, reducing the risk of a single transaction failing and
making the system more scalable and resilient.
