# Avoid Redundant Storage Access in Mutations

**Severity**: High

## Description

Improper usage of `try_mutate` leads to redundant storage operations, which can negatively impact performance. Using
both `try_mutate` and `insert` in the same closure causes unnecessary overhead by performing multiple accesses to
storage.

## What should be avoided

Using `try_mutate` followed by `insert` in a nested closure causes redundant writes:

```rust
MyStorage::<T>::try_mutate(id, |item| -> Result<(), Error> {
    *item = Some(new_value);

    // Redundant insert
    MyStorage::<T>::insert(id, new_value);

    Ok(())
});
```

## Best practice

Use either `try_mutate` to modify the value in place or `insert` alone, but avoid combining them unnecessarily:

```rust
MyStorage::<T>::try_mutate(id, |item| -> Result<(), Error> {
    *item = Some(new_value);
    Ok(())
});
```

This approach reduces storage accesses, improving both performance and resource efficiency.
