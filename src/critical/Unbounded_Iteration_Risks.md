# Unbounded Iteration Risks

**Severity**: Critical

## Description

Unbounded iterations over large data structures can lead to resource exhaustion and potential denial of service.

## Why It Should Not Be Done

```rust
for item in big_data { /* process */ }
```

## What Can Be Done Instead

Implement limits or use a bounded storage map for these iterations.

```rust
for item in big_data.iter().take(MAX_ITEMS) { /* process safely */ }
```


