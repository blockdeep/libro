# Use Deterministic Selection for Task Assignments to Prevent Manipulation

**Severity**: High

## Description

Using non-deterministic methods for assigning tasks or verifiers can create opportunities for manipulation, potentially
allowing certain participants to be chosen more frequently or unfairly.

## What Should Not Be Done

The following code relies on a random selection, which can lead to inconsistent results and potential bias:

```rust
fn assign_verifier() {
    let verifier = verifiers[rand::random::<usize>() % verifiers.len()]; // Random selection from the list
    // Task assigned to verifier unpredictably
}
```

In this example:

- `rand::random::<usize>() % verifiers.len()` selects a verifier at random, which could result in unfair frequency of
  selection for certain verifiers.

## What can be done instead

Implement a deterministic selection method, such as using the task ID as a basis to ensure a fair, repeatable selection:

```rust
fn assign_verifier_deterministic(task_id: u32) -> &Verifier {
    let index = task_id as usize % verifiers.len(); // Deterministic selection based on task ID
    &verifiers[index]
}
```

In this improved example:

- The verifier is selected based on `task_id`, ensuring that each task consistently maps to a specific verifier in a
  fair, predictable way.
- This approach prevents any single verifier from being chosen disproportionately, ensuring fair distribution and
  reducing the risk of manipulation.
