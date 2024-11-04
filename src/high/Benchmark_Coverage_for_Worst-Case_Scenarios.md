# Benchmark Coverage for Worst-Case Scenarios

**Severity**: High

**Description**: Without benchmarks for worst-case scenarios, execution weights may be underestimated.

**Why it should not be done**:

```rust
#[bench] fn typical_scenario() { /* typical path */ }
```

**What can be done instead**:

```rust
#[bench] fn worst_case_scenario() { /* cover worst path */ }
```
