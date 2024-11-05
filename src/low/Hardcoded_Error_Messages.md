# Hardcoded Error Messages

**Severity**: Low

## Description

Hardcoding error messages directly in code can make localization and future updates difficult, leading to
inconsistencies in user-facing messages.

## What Should Not Be Done

Embedding error messages directly in function logic can be inflexible:

```rust
Err("Insufficient balance".to_string())
```

## What Can Be Done Instead

Store error messages in a centralized location or use an enum for error handling:

```rust
Err(Error::<T>::InsufficientBalance)
```

This approach makes error handling more flexible, allowing for easier updates and localization.
