# Unchecked Input Data

**Severity**: Critical

**Description**: Lack of input validation can lead to unexpected behaviors and potential vulnerabilities.

**Why it should not be done**:

```rust
fn process_input(data: u32) { /* no validation */ }
```

**What can be done instead**:

```rust
fn process_input(data: u32) -> Result<(), Error> { ensure!(data < MAX_LIMIT, Error::<T>::InvalidInput); }
```
