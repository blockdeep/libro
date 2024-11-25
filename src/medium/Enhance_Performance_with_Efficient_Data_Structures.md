# Enhance Performance with Efficient Data Structures

**Severity**: <span style="color:gold;">Medium</span>

## Description

Choosing inefficient data structures can lead to suboptimal performance, especially as data scales, causing slowdowns
and increased resource usage.

## What should be avoided

Using a `Vec` for frequent lookups is often inefficient, as it requires linear-time search, which can significantly slow down performance with large data sets:

```rust
// Linear search
fn is_data_present(data: Vec<u32>, item: u32) -> bool {
    data.contains(&item)
}
```

## Best practice

### Option 1: Use more performant data structures

Consider data structures like `HashSet` or `BTreeSet` for improved lookup performance. These structures are optimized for constant or logarithmic time complexity, respectively, making them more suitable for large-scale data:

```rust
// Constant or logarithmic time search
fn is_data_present(set_data: HashSet<u32>, item: u32) -> bool
    set_data.contains(&item)
}
```

In this example:

- `set_data` provides faster, more efficient lookups, especially beneficial for large data sets.

### Option 2: Use binary search

By keeping the `Vec` sorted we can use binary search, which is a much more efficient search algorithm.

```rust
// Binary search provides a logarithmic time search.
// The array MUST be sorted.
fn is_data_present(vec_data: Vec<u32>, item: u32) -> bool {
    vec_data.binary_search(&item)
}
```

In this example:

- `vec_data` will always be sorted, and hence allows us to use the binary search algorithm for faster and efficient lookups.
