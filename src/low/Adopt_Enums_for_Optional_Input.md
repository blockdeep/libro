# Adopt Enums for Optional Input

**Severity**: <span style="color:green;">Low</span>

## Description

In Substrate development, using basic types (such as strings or integers) to represent distinct categories or optional input can lead to subtle bugs, such as typos or confusion in handling different states. Enums, on the other hand, offer a more structured approach, making it clear which values are valid and reducing the risk of errors. Using enums for representing states or categories improves both code readability and robustness, particularly in large codebases where clarity is essential.

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

Define an enum to represent distinct categories or statuses more clearly:

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

Enums make the code more robust and less prone to errors, improving readability.
