# Prevent Unnecessary Reads and Writes in Storage Access

**Severity**: <span style="color:orange;">High</span>

## Description

Unnecessary reads and writes increase execution time and storage costs, impacting performance and efficiency. Using
`try_mutate` and similar methods can reduce redundant operations by wrapping read-write logic into a single call.

## What should be avoided

Reading from and then writing to storage separately leads to redundant operations:

```rust
// Reading
let value = MyStorage::<T>::get();

// Writting
MyStorage::<T>::put(value + 1);
```

## Best practice

Use `try_mutate` or `try_mutate_exists` to combine read and write logic in a single, efficient operation:

```rust
// Reading and writting at once
MyStorage::<T>::mutate(|value| {
    value += 1;
});
```

This approach minimizes storage operations, improving both performance and resource usage.
