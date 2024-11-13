Avoid the Usage of Pseudo Random Numbers

**Severity**: <span style="color:orange;">High</span>

## Description

Using non-deterministic methods for important process such as selecting/assigning tasks for example or can create opportunities for manipulation, potentially
allowing certain participants to be chosen more frequently or unfairly.

## What should be avoided

The following code relies on a random selection, which can lead to inconsistent results and potential bias:

```rust
fn assign_verifier() {
    // Random selection from the list
    let verifier = verifiers[rand::random::<usize>() % verifiers.len()];
    // Task assigned to verifier unpredictably
}
```

In this example:

- `rand::random::<usize>() % verifiers.len()` selects a verifier at random, which could result in unfair frequency of
  selection for certain verifiers.

## Best practice

Implement a deterministic selection method, such as using the task ID as a basis to ensure a fair, repeatable selection:

```rust
fn assign_verifier_deterministic(task_id: u32) -> &Verifier {
    // Deterministic selection based on task ID
    let index = task_id as usize % verifiers.len();
    &verifiers[index]
}
```

In this improved example:

- The verifier is selected based on `task_id`, ensuring that each task consistently maps to a specific verifier in a
  fair, predictable way.
- This approach prevents any single verifier from being chosen disproportionately, ensuring fair distribution and
  reducing the risk of manipulation.