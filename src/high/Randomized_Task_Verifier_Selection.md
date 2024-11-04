# Randomized Task/Verifier Selection

**Severity**: High

## Description

Using non-deterministic methods for selection can introduce manipulation opportunities.

## Why It Should Not Be Done

```rust
fn assign_verifier() { /* random selection */ }
```

## What Can Be Done Instead

Introduce economic incentives to reward correct verifications and penalize incorrect ones.

```rust
fn assign_verifier_deterministic() { /* even distribution */ }
```


