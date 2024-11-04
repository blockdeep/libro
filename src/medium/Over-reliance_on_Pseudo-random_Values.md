# Over-reliance on Pseudo-random Values

**Severity**: Medium

## Description

Reliance on pseudo-random values can allow manipulations, risking fairness in verifier selection.

## Why It Should Not Be Done

```rust
fn select_verifier() -> Verifier { /* pseudo-random */ }
```

## What Can Be Done Instead

Adopt deterministic selection methods to ensure fairness.

```rust
fn select_verifier_deterministic() -> Verifier { /* fair distribution */ }
```


