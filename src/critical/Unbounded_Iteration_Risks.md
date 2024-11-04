# Unbounded Iteration Risks

**Severity**: Critical

**Description**: Unbounded iterations over large data structures can lead to resource exhaustion and potential denial of service.

**Why it should not be done**:

```rust
for item in big_data { /* process */ }
```

**What can be done instead**:

```rust
for item in big_data.iter().take(MAX_ITEMS) { /* process safely */ }
```
