# Avoid Hardcoded Error Messages

**Severity**: Low

## Description

Hardcoding error messages directly in code can make localization and future updates difficult, leading to
inconsistencies in user-facing messages.

## What should be avoided

Embedding error messages directly in function logic can be inflexible:

```rust
fn something_fails(){
    ...
    Err("Insufficient balance");
}
```

## What can be done instead

Store error messages in a centralized location or use an enum for error handling:

```rust
#[pallet::error]
pub enum Error<T> {
	/// The account does not have enough balance.
	InsufficientBalance,
}

fn something_fails(){
    ...
    Err(Error::<T>::InsufficientBalance);
}
```

This approach makes error handling more flexible, allowing for easier updates and localization.
