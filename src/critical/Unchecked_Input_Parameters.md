# Unchecked Input Parameters

**Severity**: <span style="color:red;">Critical</span>

## Description

In Substrate runtime development, lack of input validation can lead to vulnerabilities and unexpected behaviors. Unverified inputs might result in invalid states, security issues, or exploitation by malicious actors, disrupting the normal operation of the blockchain.

## What should be avoided

The following code accepts input without validating its range or format, which can lead to unintended results:

```rust
fn store_execution_time(hour_of_day: u8) {
    ExecutedAt::<T>::insert(hour_of_day);
}
```

In this example:

- The `hour_of_day` input should only be valid if it is between 0 and 23 hours. Otherwise, the input is invalid and should return an error.

## Recommended Solution

Implement input validation to ensure data meets expected constraints. This example enforces a maximum limit to avoid out-of-range values:

```rust
fn store_execution_time(hour_of_day: u8) -> Result<(), Error> {
    // Validate input before processing
    ensure!(hour_of_day <= 23, Error::<T>::TimeOutOfRange);

    ExecutedAt::<T>::insert(hour_of_day);
    Ok(())
}
```

By validating inputs, we prevent potentially harmful values from entering the system, enhancing reliability and security.
