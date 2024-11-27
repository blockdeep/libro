# Avoid Hardcoded Error Messages

**Severity**: <span style="color:green;">Low</span>

## Description

Hardcoding error messages directly in Substrate code can make it difficult to manage and update error handling across the runtime. When error messages are embedded within function logic, localization becomes cumbersome, and updating messages in the future may lead to inconsistencies. By using enums for error handling, developers can centralize and standardize error messages, making the code more flexible, easier to maintain, and adaptable to future changes, including localization for different languages or regions.

## What should be avoided

Embedding error messages directly in function logic can be inflexible:

```rust
fn something_fails() -> Result<(), Error> {
    // ...
    Err("Insufficient balance")
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

fn something_fails() -> DispatchError<()> {
    // ...
    Err(Error::<T>::InsufficientBalance)
}
```

This approach makes error handling more flexible, allowing for easier updates and localization.
