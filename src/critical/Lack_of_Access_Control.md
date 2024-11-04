# Lack of Access Control

**Severity**: Critical

**Description**: Open access on extrinsics without checks may allow unauthorized actions that can compromise platform security.

**Why it should not be done**:

```rust
pub fn execute() { /* open access */ }
```

**What can be done instead**:

```rust
pub fn execute(origin: OriginFor<T>) -> DispatchResult { ensure_root(origin)?; /* secure access */ }
```
