# Unchecked Input Parameters

**Severity**: <span style="color:red;">Critical</span>

## Description

Lack of input validation can lead to unexpected behaviors and vulnerabilities, as unverified inputs might cause invalid
states or security issues.

## What should be avoided

The following code accepts input without validating its range or format, which can lead to unintended results:

**TODO: The code snippet should have more code and must show what's wrong here.**

```rust
fn store_execution_time(hour_of_day: u32) {
    ExecutedAt::insert(hour_of_day)
}
```

In this example:

- The `hour_of_day` input should only be valid if it's between 0 and 24 hours otherwise the input is invalid and should return an error.

## Recommended Solution

Implement input validation to ensure data meets expected constraints. This example enforces a maximum limit to avoid
out-of-range values:

```rust
fn store_execution_time(hour_of_day: u32) -> Result<(), Error> {
    // Validate input before processing
    ensure!(hour_of_day <= 24, Error::<T>::TimeOutOfRange);
    Ok(())
}
```

By validating inputs, we prevent potentially harmful values from entering the system, enhancing reliability and
security.
