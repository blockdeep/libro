# Frontend-Agnostic Considerations

**Severity**: Informational

## Description

The use of frontend-specific values may conflict with backend design.

## What should not be done

```rust
fn display_value() { /* frontend-specific */ }
```

## What Can Be Done Instead

Ensure backend remains frontend-agnostic to avoid inconsistencies.

```rust
fn display_value_generic() { /* backend-agnostic */ }
```


