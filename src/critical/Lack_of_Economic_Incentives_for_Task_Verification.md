# Lack of Economic Incentives for Task Verification

**Severity**: Critical

## Description
Without proper incentives, verifiers may lack motivation to perform accurate validations, risking system reliability.

## Why It Should Not Be Done

The following code demonstrates a poor practice that can lead to issues:

```rust
fn verify_task(task_id: u32) -> bool { /* verifier decides without incentive */ }
```

In this example:
- Explain the potential issue or lack of protection mechanisms.

## What Can Be Done Instead

An improved version is shown below:

```rust
fn verify_task_with_incentive(task_id: u32) -> Result<bool, DispatchError> { /* incentivized verifier logic */ }
```

Explanation:
- Detail how the changes provide safeguards or improvements.
