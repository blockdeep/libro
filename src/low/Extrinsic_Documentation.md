# Extrinsic Documentation

**Severity**: Low

## Description
Extrinsics without documentation can lead to confusion regarding their use.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
pub fn transfer() { /* no docs */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
/// Transfers assets from sender to recipient
pub fn transfer() { /* documented */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
