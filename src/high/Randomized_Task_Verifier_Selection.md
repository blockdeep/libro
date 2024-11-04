# Randomized Task/Verifier Selection

**Severity**: High

## Description
Using non-deterministic methods for selection can introduce manipulation opportunities.

## Why It Should Not Be Done


```rust
fn assign_verifier() { /* random selection */ }
```



## What Can Be Done Instead



```rust
fn assign_verifier_deterministic() { /* even distribution */ }
```


