# Frontend-Agnostic Considerations

**Severity**: Informational

## Description
The use of frontend-specific values may conflict with backend design.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn display_value() { /* frontend-specific */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn display_value_generic() { /* backend-agnostic */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
