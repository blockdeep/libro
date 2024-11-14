# Enhance Logging in Migration Scripts

**Severity**: <span style="color:gold;">Medium</span>

## Description

Logging messages in migration scripts should provide clear and specific information about the migration process. Adding
more explicit logs helps track progress, identify issues, and understand the migration flow.

## What should be avoided

Using general log messages in migration scripts provides minimal information:

```rust
log::info!("Migration started");
```

## Best practice

Use more detailed logging, including migration-specific information and conditions:

```rust
log::info!("Migration started for version: {}", current_version);
if let Some(bucket) = translate(process) {
    log::info!("Translated bucket data for migration: {:?}", bucket);
} else {
    log::warn!("Translation process returned None for bucket data");
}
```

In this example:

- Each log message includes specific information, making it easier to trace migration steps and identify issues if they
  occur.
