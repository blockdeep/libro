# Implement Descriptive Logging

**Severity**: Low

## Description

Without descriptive logging, debugging and monitoring issues become challenging, as the log entries may lack context or
detail.

## What should be avoided

Logging messages without context or specific details can make troubleshooting challenging and time-consuming:

```rust
log::info!("Process started");
```

## Best Practice

Add context and relevant details to log messages to improve clarity and facilitate debugging:

```rust
const LOG_TARGET: &str = "pallet-logging";
log::info!(LOG_TARGET, "Process started for user: {:?}", user_id);
```

This approach enhances traceability, readability, and the overall effectiveness of the logging system by providing meaningful information in each log entry.
