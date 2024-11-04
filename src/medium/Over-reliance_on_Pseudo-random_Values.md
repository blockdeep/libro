# Avoid Over-reliance on Pseudo-random Values to Ensure Fairness

**Severity**: Medium

## Description

Relying on pseudo-random values for critical operations, such as selecting verifiers or validators, can allow for
manipulation, potentially leading to unfair or biased outcomes. Adopting deterministic methods ensures a predictable and
fair distribution.

## What Should Not Be Done

Using pseudo-random values for selection can lead to inconsistent and potentially biased outcomes:

```rust
fn select_verifier() -> Verifier {
    let index = generate_random_number() % verifiers.len(); // Pseudo-randomly selects a verifier
    verifiers[index]
}
```

In this example:

- The verifier selection is based on a pseudo-random index, which may favor certain verifiers over others, especially if
  the randomness source is predictable.

## What Can Be Done Instead

Use a deterministic approach to ensure fair distribution across all participants, such as by hashing a unique
identifier:

```rust
fn select_verifier_deterministic(task_id: u32) -> Verifier {
    let index = (task_id as usize) % verifiers.len(); // Deterministically selects a verifier based on task ID
    verifiers[index]
}
```

In this improved example:

- The `task_id` is used to create a consistent, repeatable index for verifier selection, ensuring each task maps to a
  specific verifier in a fair and predictable way.
- This deterministic approach prevents favoritism and reduces the risk of manipulation, promoting fairness in critical
  operations.
