# Missing Extrinsic Documentation

**Severity**: Medium

## Description

Lack of extrinsic documentation can cause misunderstandings regarding usage permissions, inputs, and error handling.

## Why It Should Not Be Done

```rust
fn some_extrinsic() { /* undocumented extrinsic */ }
```

## What Can Be Done Instead

Document conditions, possible errors, and permissions for extrinsics.

```rust
/// Performs operation. 
/// Params: description of each parameter
fn documented_extrinsic() { /* documented extrinsic */ }
```


