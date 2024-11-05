# Insufficient Use of Enumerations

**Severity**: Low

## Description

Using basic types (e.g., strings, integers) instead of enumerations for distinct categories or statuses can lead to
errors and make the code less readable.

## What Should Not Be Done

Using a string or integer to represent distinct categories increases the risk of typos and confusion:

```rust
let status = "completed"; // Using string literals for statuses
```

## What Can Be Done Instead

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
