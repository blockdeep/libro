# Unchecked Input Data

**Severity**: Critical

## Description

Lack of input validation can lead to unexpected behaviors and vulnerabilities, as unverified inputs might cause invalid
states or security issues.

## What should not be done

The following code accepts input without validating its range or format, which can lead to unintended results:

```rust
fn process_input(data: u32) {
    // Processes data with no validation
}
```

## What can be done instead

Implement input validation to ensure data meets expected constraints. This example enforces a maximum limit to avoid
out-of-range values:

```rust
fn process_input(data: u32) -> Result<(), Error> {
    // Validate input before processing
    ensure!(data < MAX_LIMIT, Error::<T>::InvalidInput);
    Ok(())
}
```

By validating inputs, we prevent potentially harmful values from entering the system, enhancing reliability and
security.
