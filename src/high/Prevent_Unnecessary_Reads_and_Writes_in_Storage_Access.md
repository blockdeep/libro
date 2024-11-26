# Prevent Unnecessary Reads and Writes in Storage Access

**Severity**: <span style="color:orange;">High</span>

## Description

Accessing and writing to blockchain storage is resource-intensive due to the I/O cost of interacting with disk-backed or serialized structures and the algorithmic overhead of traversing key-value stores. Each read and write contributes to execution weight and transaction fees, making redundant operations inefficient and costly. These inefficiencies can degrade performance, reduce scalability, and increase user costs, as storage operations are among the most expensive in a runtime. Combining read and write logic into a single operation minimizes these costs, improving overall system efficiency and predictability.

Unnecessary reads and writes increase execution time and storage costs, impacting performance and efficiency. In a blockchain context, where every operation contributes to the overall transaction weight and cost, optimizing storage access is critical. Using `try_mutate` and similar methods allows you to wrap read-write logic into a single call, reducing the overhead associated with separate operations.

## What should be avoided

Reading from and then writing to storage separately leads to redundant operations:

```rust
// Reading
let value = MyStorage::<T>::get();

// Writing
MyStorage::<T>::put(value + 1);
```

This pattern involves two storage accesses—one for reading and another for writing—resulting in increased computational and I/O costs.

## Best practice

Use `try_mutate` or `try_mutate_exists` to combine read and write logic in a single, efficient operation:

```rust
// Reading and writing at once
MyStorage::<T>::mutate(|value| {
    value += 1;
});
```

This approach minimizes storage operations, improving both performance and resource usage. By consolidating the read and write into a single call, you ensure that the execution weight remains low while maintaining predictable and efficient storage access patterns.
