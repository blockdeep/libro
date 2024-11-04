# Frontend-Agnostic Considerations

**Severity**: Informational

## Description
The use of frontend-specific values may conflict with backend design.

## Why It Should Not Be Done


```rust
fn display_value() { /* frontend-specific */ }
```



## What Can Be Done Instead



```rust
fn display_value_generic() { /* backend-agnostic */ }
```


