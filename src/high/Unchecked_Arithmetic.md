# Unchecked Arithmetic

**Severity**: High

**Description**: Unchecked arithmetic operations can lead to overflow errors.

**Why it should not be done**:

```rust
let total = a + b;
```

**What can be done instead**:

```rust
let total = a.checked_add(b).ok_or(Error::<T>::Overflow)?;
```
