# Include Error Documentation

**Severity**: Medium

## Description

Lack of documentation on error variants can make it challenging for developers to understand and address issues. Adding
documentation for each error provides valuable context in code metadata, making it easier to identify the cause of
failures.

## What should be avoided

Leaving error variants undocumented can lead to confusion and slow down debugging:

```rust
#[pallet::error]
pub enum Error {
    InsufficientBalance,
    InvalidAsset,
}
```

In this example:

- No documentation is provided for the error variants inside the `Error` enum.

## Best practice

Add documentation for each error variant to clarify its cause and expected behavior:

```rust
#[pallet::error]
pub enum Error {
    /// Occurs when the user's balance is too low for the operation.
    InsufficientBalance,
    /// Indicates that the specified asset is not recognized.
    InvalidAsset,
}
```

In this example:

- Documenting each error variant provides more context, helping developers understand the cause and appropriate response
  for each error.
