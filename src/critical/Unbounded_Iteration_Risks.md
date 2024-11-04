# Unbounded Iteration Risks

**Severity**: Critical

## Description
Unbounded iterations over large data structures can lead to resource exhaustion and potential denial of service.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
for item in big_data { /* process */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
for item in big_data.iter().take(MAX_ITEMS) { /* process safely */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
