# Modularization of Large Files

**Severity**: Medium

**Description**: Large files reduce readability and make navigation difficult for developers.

**Why it should not be done**:

```rust
// single large file with multiple functions
```

**What can be done instead**:

```rust
// split functions into smaller modules
```
