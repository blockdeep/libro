# Implement Descriptive Logging

**Severity**: <span style="color:green;">Low</span>

## Description

In Substrate runtime development, logging is an essential tool for monitoring and debugging. Without descriptive and contextual logging, it becomes difficult to trace the flow of operations or identify issues effectively. Log messages that lack sufficient detail can make troubleshooting slow and inefficient, especially when dealing with complex or production-grade systems. By implementing descriptive logging, developers provide valuable insights that can help quickly diagnose problems, track system behavior, and improve the overall maintainability and observability of the blockchain runtime.

## What should be avoided

Logging messages without context or specific details can make troubleshooting challenging and time-consuming:

```rust
log::info!("Process started");
```

## Best practice

Add context and relevant details to log messages to improve clarity and facilitate debugging:

```rust
const LOG_TARGET: &str = "pallet-logging";
log::info!(LOG_TARGET, "Process started for user: {:?}", user_id);
```

This approach enhances traceability, readability, and the overall effectiveness of the logging system by providing meaningful information in each log entry.
