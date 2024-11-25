# Adopt Enumerations for Clearer Code

**Severity**: <span style="color:green;">Low</span>

## Description

Using basic types (e.g., strings, integers) instead of enumerations for distinct categories or statuses can lead to
errors and make the code less readable.

## What should be avoided

Using a string or integer to represent distinct categories increases the risk of typos and confusion:

```rust
// Using string literals for statuses
let mut status = "pending";

status = if condition {
    "completed"
} else {
    "aborted"
}
```

## Best practice

Define an enumeration to represent distinct categories or statuses more clearly:

```rust
enum Status {
    /// The operation is still being confirmed and can potentially be aborted.
    Pending,
    /// The operation has been confirmed and it is waiting to be completed.
    InProgress,
    // The operation was successfully completed.
    Completed,
    /// The operation was manually aborted by the user.
    Aborted,
}

let mut status = Status::Pending;

status = if condition {
    Status::Completed
} else {
    Status::Aborted
}
```

Enumerations make the code more robust and less prone to errors, improving readability.
