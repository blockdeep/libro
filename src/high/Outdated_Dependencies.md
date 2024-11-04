# Outdated Dependencies

**Severity**: High

**Description**: Using outdated libraries may lead to security and compatibility issues.

**Why it should not be done**:

```rust
use outdated_library::deprecated_fn;
```

**What can be done instead**:

```rust
use latest_library::safe_fn;
```
