# Use of Safe Math

**Severity**: Medium

## Description

Unchecked arithmetic operations can lead to overflow errors.

## What should not be done

```rust
let total = a + b;
```

## What Can Be Done Instead

Use safe math functions for all arithmetic operations.

```rust
let total = a.checked_add(b).ok_or(Error::<T>::Overflow)?;
```


