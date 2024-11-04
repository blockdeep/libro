# Naming Conventions

**Severity**: Low

**Description**: Inconsistent or ambiguous naming conventions reduce code readability.

**Why it should not be done**:

```rust
fn processData() { /* vague name */ }
```

**What can be done instead**:

```rust
fn process_transaction_data() { /* descriptive name */ }
```
