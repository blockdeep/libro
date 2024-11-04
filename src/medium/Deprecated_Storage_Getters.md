# Deprecated Storage Getters

**Severity**: Medium

## Description

Using deprecated storage getters may lead to compatibility issues in future versions.

## Why It Should Not Be Done

```rust
let value = Storage::<T>::get();
```

## What Can Be Done Instead

Replace deprecated getters with recommended methods.

```rust
let value = Storage::<T>::try_get()?;
```


