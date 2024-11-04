# Missing Extrinsic Documentation

**Severity**: Medium

## Description
Lack of extrinsic documentation can cause misunderstandings regarding usage permissions, inputs, and error handling.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn some_extrinsic() { /* undocumented extrinsic */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
/// Performs operation. 
 /// Params: description of each parameter
 fn documented_extrinsic() { /* documented extrinsic */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
