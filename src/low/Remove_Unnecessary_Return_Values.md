# Remove Unnecessary Return Values

**Severity**: Low

## Description

Returning values that are not modified or required by the function can clutter the code, leading to inefficiencies and
reducing readability. Removing these unnecessary return values simplifies function signatures and clarifies function
purpose.

## What should be avoided

Returning an input parameter without modification is redundant and can be confusing:

```rust
fn project_validation(project_metadata: Metadata) -> Metadata {
    // Perform validation
    // ...

    // Returns the same value without changes
    project_metadata
}
```

## Best practice

If the return value is not needed, avoid returning it, focusing the function solely on its primary operation:

```rust
fn project_validation(project_metadata: &Metadata) -> Result<(), Error> {
    // Perform validation without returning project_metadata

    Ok(())
}
```

In this approach:

- The function is more straightforward, focusing only on validation without an unnecessary return value, improving
  clarity and maintainability.
