# Enhance Performance with Efficient Data Structures

**Severity**: <span style="color:gold;">Medium</span>

## Description

Choosing inefficient data structures can lead to suboptimal performance, especially as data scales, causing slowdowns and increased resource usage. In Substrate runtime development, where performance is critical, inefficient operations can increase block execution time, reduce throughput, and lead to higher transaction costs.

This is a broad concept, and developers should select data structures suited to their specific use cases. Below are basic examples to highlight common pitfalls and improvements.

## What should be avoided

Using a `Vec` for frequent lookups is often inefficient, as it requires linear-time search, which can significantly slow down performance with large data sets:

```rust
// Linear search
fn is_data_present(data: Vec<u32>, item: u32) -> bool {
    data.contains(&item)
}
```

In this example:

- The `Vec` requires scanning all elements in the worst case, leading to poor performance as the data set grows.

## Best practice

### Option 1: Use more performant data structures

Data structures like `HashSet` or `BTreeSet` are optimized for faster lookups, with constant or logarithmic time complexity, respectively. These are better suited for scenarios requiring frequent membership checks or updates.

```rust
use std::collections::HashSet;

// Constant or logarithmic time search
fn is_data_present(set_data: HashSet<u32>, item: u32) -> bool {
    set_data.contains(&item)
}
```

In this example:

- `set_data` enables faster and more efficient lookups, improving performance for large data sets.

### Option 2: Use binary search

If you must use a `Vec`, keeping it sorted allows for binary search, which reduces the time complexity to logarithmic.

```rust
// Binary search provides a logarithmic time search.
// The array MUST be sorted.
fn is_data_present(vec_data: &[u32], item: u32) -> bool {
    vec_data.binary_search(&item).is_ok()
}
```

In this example:

- A sorted `Vec` allows for efficient binary search, combining the simplicity of a `Vec` with improved lookup performance.

By choosing the right data structure or optimizing the existing one, developers can ensure efficient execution, scalability, and reduced resource usage in their runtime logic.
