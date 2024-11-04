# Undefined Storage Limits in Marketplace Offers

**Severity**: High

## Description
Allowing unlimited offers can lead to storage overflow and high costs during clearing operations.

## Why It Should Not Be Done


```rust
fn add_offer(offer: Offer) { /* unlimited entries */ }
```



## What Can Be Done Instead



```rust
fn add_offer_limited(offer: Offer) { /* enforce offer limits */ }
```


