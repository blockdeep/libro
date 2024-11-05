# Lack of Descriptive Logging

**Severity**: Low

## Description

Without descriptive logging, debugging and monitoring issues become challenging, as the log entries may lack context or
detail.

## What should not be done

Logging messages without context or relevant details makes troubleshooting difficult:

```rust
log::info!("Process started");
```

## What Can Be Done Instead

Include context and relevant details in log messages to enhance debugging:

```rust
const LOG_TARGET: &str = "pallet-logging";
log::info!(LOG_TARGET, "Process started for user: {:?}", user_id);
```

This approach improves traceability and enhances readability.
