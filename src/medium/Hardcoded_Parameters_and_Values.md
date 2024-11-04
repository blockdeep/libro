# Hardcoded Parameters and Values

**Severity**: Medium

## Description
Hardcoding parameters can reduce flexibility, making it harder to adapt to different environments.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
const LIMIT: u32 = 100;
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
pub trait Config: frame_system::Config { const LIMIT: u32; }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
