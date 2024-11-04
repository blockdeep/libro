# Avoid Unbounded Iterations to Prevent Resource Exhaustion

**Severity**: Critical

## Description

Unbounded iterations over large data structures can lead to resource exhaustion and may result in denial of service (
DoS) attacks if the process consumes too many resources.

## What should not be done

The following code iterates over all items in `big_data` without any limit, which can overwhelm system resources if
`big_data` is large:

```rust
for item in big_data {
    // Process each item with no limit
}
```

## What can be done instead

Use a bounded iterator or limit the number of items processed in each iteration. This approach prevents excessive
resource usage and keeps operations predictable.

```rust
for item in big_data.iter().take(MAX_ITEMS) {
    // Process a limited number of items safely
}
```

By setting a maximum limit, we can control the processing load and avoid potential performance issues.
