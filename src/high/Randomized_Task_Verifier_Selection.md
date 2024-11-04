# Randomized Task/Verifier Selection

**Severity**: High

## Description
Using non-deterministic methods for selection can introduce manipulation opportunities.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn assign_verifier() { /* random selection */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn assign_verifier_deterministic() { /* even distribution */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
