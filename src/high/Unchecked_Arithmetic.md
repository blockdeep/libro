# Unchecked Arithmetic

**Severity**: High

## Description

Unchecked arithmetic operations can lead to overflow errors.

## What should not be done

```rust
let total = a + b;
```

## What Can Be Done Instead

```rust
let total = a.checked_add(b).ok_or(Error::<T>::Overflow)?;
```


