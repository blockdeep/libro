# Deprecated Storage Getters

**Severity**: Medium

**Description**: Using deprecated storage getters may lead to compatibility issues in future versions.

**Why it should not be done**:

```rust
let value = Storage::<T>::get();
```

**What can be done instead**:

```rust
let value = Storage::<T>::try_get()?;
```
