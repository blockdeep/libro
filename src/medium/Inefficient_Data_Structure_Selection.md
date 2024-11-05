# Inefficient Data Structure Selection

**Severity**: Medium

## Description

Choosing inefficient data structures can lead to suboptimal performance, especially as data scales, causing slowdowns
and increased resource usage.

## What Should Not Be Done

Using a `Vec` for frequent lookups, which requires linear-time search, can slow down performance in large data sets:

```rust
let result = vec_data.contains(&item); // Linear search
```

## What Can Be Done Instead

Use a `HashSet` or `BTreeSet` for efficient lookup operations:

```rust
let result = set_data.contains(&item); // Constant or logarithmic time search
```

In this example:

- `set_data` provides faster, more efficient lookups, especially beneficial for large data sets.
