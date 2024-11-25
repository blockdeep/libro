# Include Tests for Edge Cases

**Severity**: <span style="color:gold;">Medium</span>

## Description

Omitting tests for boundary cases can leave critical edge conditions unhandled, leading to potential bugs and
unpredictable behavior, especially when inputs approach their limits.

## What should be avoided

Neglecting boundary cases in testing may overlook issues that occur at the extremes of expected input ranges:

```rust
#[test]
fn test_process_data() {
    // Typical case
    assert_eq!(process_data(50), Some(50));
}
```

In this example:

- The function only tests a typical case (`50`) and misses important edge conditions that could cause issues if
  unhandled.

## Best practice

Include tests for boundary conditions to verify that the code handles edge cases, such as zero, maximum, and just beyond
maximum values:

```rust
#[test]
fn test_process_data_with_boundary_cases() {
    // Minimum boundary
    assert_eq!(process_data(0), Some(0));

    // Maximum boundary
    assert_eq!(process_data(MAX_LIMIT), Some(MAX_LIMIT));

    // Beyond maximum boundary
    assert!(process_data(MAX_LIMIT + 1).is_none());
}
```

In this improved example:

- We test the function at `0` (minimum boundary), `MAX_LIMIT` (maximum boundary), and `MAX_LIMIT + 1` (just beyond the
  maximum).
- This ensures that `process_data` behaves correctly at all crucial boundaries, improving robustness and reducing the
  risk of bugs in production.
