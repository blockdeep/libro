# Inconsistent State after Token Transfers

**Severity**: High

## Description
Relying on the last buyer to cover delivery costs for previous buyers risks penalties and errors.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn finalize_purchase() { /* delivery for all */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn finalize_purchase_sequential() { /* claim-based delivery */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
