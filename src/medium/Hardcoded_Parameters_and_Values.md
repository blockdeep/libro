# Hardcoded Parameters and Values

**Severity**: Medium

## Description

Hardcoding parameters can reduce flexibility, making it harder to adapt to different environments.

## What should not be done

```rust
const LIMIT: u32 = 100;
```

## What Can Be Done Instead

Use configurable parameters to enhance adaptability.

```rust
pub trait Config: frame_system::Config { const LIMIT: u32; }
```


