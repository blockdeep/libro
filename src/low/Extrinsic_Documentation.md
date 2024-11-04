# Extrinsic Documentation

**Severity**: Low

## Description

Extrinsics without documentation can lead to confusion regarding their use.

## Why It Should Not Be Done

```rust
pub fn transfer() { /* no docs */ }
```

## What Can Be Done Instead

Provide detailed documentation for each extrinsic, including functionality and parameters.

```rust
/// Transfers assets from sender to recipient
pub fn transfer() { /* documented */ }
```


