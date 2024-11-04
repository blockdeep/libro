# Lack of Access Control

**Severity**: Critical

## Description
Open access on extrinsics without checks may allow unauthorized actions that can compromise platform security.

## Why It Should Not Be Done


```rust
pub fn execute() { /* open access */ }
```



## What Can Be Done Instead



```rust
pub fn execute(origin: OriginFor<T>) -> DispatchResult { ensure_root(origin)?; /* secure access */ }
```
