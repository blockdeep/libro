# Maintain Consistent Documentation Standards

**Severity**: <span style="color:cyan;">Informational</span>

## Description

Inconsistent documentation standards can lead to confusion and hinder understanding, making it more challenging for developers—especially new contributors—to work with the codebase. Proper documentation ensures that each function, module, and component is well-understood and easily navigable. By adhering to a consistent documentation standard, developers ensure clarity, reduce the likelihood of errors, and make the code more maintainable, fostering better collaboration and smoother onboarding for new team members. To understand best practices in documentation, it is helpful to refer to how FRAME pallets are developed, as they follow a robust and standardized approach to both coding and documenting, ensuring consistency across the entire Substrate ecosystem. Taking a look at FRAME pallets can provide insight into how comprehensive documentation improves maintainability and collaboration in larger projects.

## What should be avoided

Lack of documentation or minimal comments can leave important details unclear, as shown below:

```rust
fn process_data(data: u32) -> u32 {
  // Function logic here
  // ...
}
```

In this example:

- The function lacks a description of its purpose, parameters, and potential side effects, making it difficult for others to understand, use or modify it confidently.

## Best practice

Establish a consistent documentation standard that includes detailed descriptions, parameter explanations, and expected outcomes for each function.

```rust
/// Processes the provided data by performing necessary calculations.
///
/// # Parameters
/// - `data`: The input data to be processed, expected as an unsigned integer.
///
/// # Returns
/// - Result of the processing operation as a `u32`.
fn process_data(data: u32) -> u32 {
    // Function logic here
    // ...
}
```

With a standardized documentation format, each function is clearly explained, making the codebase easier to understand and maintain. This approach reduces the risk of misinterpretation and supports team collaboration.
