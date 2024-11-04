# Benchmark Coverage for Worst-Case Scenarios

**Severity**: High

## Description

Without benchmarks for worst-case scenarios, execution weights may be underestimated.

## What should not be done

```rust
#[bench] fn typical_scenario() { /* typical path */ }
```

## What Can Be Done Instead

Benchmark worst-case paths and update extrinsics to reflect these cases accurately.

```rust
#[bench] fn worst_case_scenario() { /* cover worst path */ }
```


