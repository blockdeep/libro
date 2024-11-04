# Inconsistent State after Token Transfers

**Severity**: High

## Description

Relying on the last buyer to cover delivery costs for previous buyers risks penalties and errors.

## What should not be done

```rust
fn finalize_purchase() { /* delivery for all */ }
```

## What Can Be Done Instead

Use a claim-based delivery process or batch processing.

```rust
fn finalize_purchase_sequential() { /* claim-based delivery */ }
```


