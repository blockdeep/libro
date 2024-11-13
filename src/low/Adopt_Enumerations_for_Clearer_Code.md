# Adopt Enumerations for Clearer Code

**Severity**: <span style="color:green;">Low</span>

## Description

Using basic types (e.g., strings, integers) instead of enumerations for distinct categories or statuses can lead to
errors and make the code less readable.

## What should be avoided

Using a string or integer to represent distinct categories increases the risk of typos and confusion:

```rust
// Using string literals for statuses
let status = "completed";
```

## Best practice

Define an enumeration to represent distinct categories or statuses more clearly:

```rust
enum Status {
    Pending,
    InProgress,
    Completed,
}

let status = Status::Completed;
```

Enumerations make the code more robust and less prone to errors, improving readability.