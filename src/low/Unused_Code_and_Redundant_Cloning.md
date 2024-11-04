# Unused Code and Redundant Cloning

**Severity**: Low

**Description**: Redundant code and cloning increase code size and decrease efficiency.

**Why it should not be done**:

```rust
let data = my_data.clone();
```

**What can be done instead**:

```rust
let data = &my_data;
```
