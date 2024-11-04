# Randomized Task/Verifier Selection

**Severity**: High

## Description

Using non-deterministic methods for selection can introduce manipulation opportunities.

## What should not be done

```rust
fn assign_verifier() { /* random selection */ }
```

## What Can Be Done Instead

Introduce economic incentives to reward correct verifications and penalize incorrect ones.

```rust
fn assign_verifier_deterministic() { /* even distribution */ }
```


