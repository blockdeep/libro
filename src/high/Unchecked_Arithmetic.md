# Unchecked Arithmetic

**Severity**: High

## Description
Unchecked arithmetic operations can lead to overflow errors.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
let total = a + b;
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
let total = a.checked_add(b).ok_or(Error::<T>::Overflow)?;
```

Explanation:
- Detail how the changes provide safeguards or improvements.
