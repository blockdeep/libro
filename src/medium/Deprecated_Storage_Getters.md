# Deprecated Storage Getters

**Severity**: Medium

## Description
Using deprecated storage getters may lead to compatibility issues in future versions.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
let value = Storage::<T>::get();
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
let value = Storage::<T>::try_get()?;
```

Explanation:
- Detail how the changes provide safeguards or improvements.
