# Unvalidated External Data

**Severity**: High

## Description

Failing to validate external data, such as user inputs or API responses, can lead to unexpected behavior and
vulnerabilities.

## What Should Not Be Done

Using external data directly without validation:

```rust
let amount = external_input.parse::<u32>().unwrap();
```

## What Can Be Done Instead

Validate and handle external data safely to prevent errors or potential injection attacks:

```rust
let amount = external_input.parse::<u32>().map_err(|_| Error::<T>::InvalidInput)?;
```

In this example:

- Input validation ensures that only acceptable data formats are processed, reducing error risks.
