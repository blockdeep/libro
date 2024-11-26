# Enhance Logging in Migration Scripts

**Severity**: <span style="color:gold;">Medium</span>

## Description

Logging messages in migration scripts should provide clear and specific information about the migration process. In Substrate-based blockchains, where migrations often involve updating on-chain state, detailed logs are critical for tracking progress, diagnosing issues, and ensuring transparency during the process. Insufficient logging can make it difficult to pinpoint errors or understand the steps taken during a migration.

## What should be avoided

Using general log messages in migration scripts provides minimal information:

```rust
log::info!("Migration started");
```

In this example:

- The log message gives no indication of what migration is running, what data is being processed, or whether specific conditions were met, making debugging and tracking nearly impossible.

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

- Each log message includes specific information, making it easier to trace migration steps and identify issues if they occur.
