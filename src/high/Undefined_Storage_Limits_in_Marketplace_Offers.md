# Undefined Storage Limits in Marketplace Offers

**Severity**: High

## Description
Allowing unlimited offers can lead to storage overflow and high costs during clearing operations.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn add_offer(offer: Offer) { /* unlimited entries */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn add_offer_limited(offer: Offer) { /* enforce offer limits */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
