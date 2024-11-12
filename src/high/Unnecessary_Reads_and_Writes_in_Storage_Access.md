# Prevent Unnecessary Reads and Writes in Storage Access

**Severity**: High

## Description

Unnecessary reads and writes increase execution time and storage costs, impacting performance and efficiency. Using
`try_mutate` and similar methods can reduce redundant operations by wrapping read-write logic into a single call.

## What should be avoided

Reading from and then writing to storage separately leads to redundant operations:

```rust
let mut value = MyStorage::<T>::get();
value += 1;
MyStorage::<T>::put(value);
```

## Best Practice

Use `try_mutate` or `try_mutate_exists` to combine read and write logic in a single, efficient operation:

```rust
MyStorage::<T>::try_mutate(|value| -> Result<(), Error> {
    value.saturating_add(One::one());
    Ok(())
})?;
```

This approach minimizes storage operations, improving both performance and resource usage.
