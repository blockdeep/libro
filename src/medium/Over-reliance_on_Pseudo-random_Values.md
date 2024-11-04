# Over-reliance on Pseudo-random Values

**Severity**: Medium

## Description
Reliance on pseudo-random values can allow manipulations, risking fairness in verifier selection.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn select_verifier() -> Verifier { /* pseudo-random */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn select_verifier_deterministic() -> Verifier { /* fair distribution */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
