# Avoid Unwrap Usage Inside Runtime

**Severity**: <span style="color:red;">Critical</span>

## Description

Using `unwrap()` and similar methods for error handling can cause runtime panics, leading to crashes if unexpected
conditions arise. Explicit error handling provides more robust and predictable behavior, especially in production
environments.

## What should be avoided

Using `unwrap()` for error handling can result in runtime panics, which are not user-friendly and may lead to unexpected
application crashes:

```rust
let my_data = Vec::<u32>::new();

// Potential panic if index 0 is empty
let value = my_data.get(0).unwrap();

// Same error, with implicit unwrapping
let value = my_data[0];
```

## Best practice

Handle errors explicitly by using `Result` and provide descriptive error messages:

```rust
let my_data = Vec::<u32>::new();

// Gracefully handling the error
let value = my_data.get(0).ok_or(Error::<T>::MyError)?;
```

In this example:

- The code safely handles the case where `my_data.get(0)` might be `None`, allowing for graceful error handling and
  reducing the risk of crashes.
