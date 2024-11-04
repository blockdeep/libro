# Randomized Task/Verifier Selection

**Severity**: High

**Description**: Using non-deterministic methods for selection can introduce manipulation opportunities.

**Why it should not be done**:

```rust
fn assign_verifier() { /* random selection */ }
```

**What can be done instead**:

```rust
fn assign_verifier_deterministic() { /* even distribution */ }
```
