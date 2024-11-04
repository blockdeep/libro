# Hardcoded Parameters

**Severity**: Medium

**Description**: Hardcoding parameters can reduce flexibility, making it harder to adapt to different environments.

**Why it should not be done**:

```rust
const LIMIT: u32 = 100;
```

**What can be done instead**:

```rust
pub trait Config: frame_system::Config { const LIMIT: u32; }
```
