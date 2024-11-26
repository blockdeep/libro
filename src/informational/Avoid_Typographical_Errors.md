# Avoid Typographical Errors

**Severity**: <span style="color:cyan;">Informational</span>

## Description

Typographical errors, while often overlooked, can significantly affect the clarity and professionalism of a Substrate codebase. In a decentralized environment where precision is critical, such errors can lead to confusion, incorrect assumptions, and even subtle bugs. Whether in variable names, comments, or documentation, ensuring accuracy in spelling helps maintain clear communication within the team and with external contributors, reducing the likelihood of misunderstandings and improving the overall quality of the project.

## What should be avoided

Typographical errors can make code less readable and may even lead to bugs if used inconsistently:

```rust
// Typo in variable name.
let amout_valu = 100;
```

In this example:

- The misspelled variable `amout_valu` is unclear and could lead to confusion, especially if referenced in multiple parts of the code.

## Best practice

Perform thorough proofreading to catch typos and enhance clarity, ensuring variable names and comments are accurate and descriptive.

```rust
// Correctly spelled variable name.
let amount_value = 100;
```

Using clear and correctly spelled names improves readability, maintains professionalism, and helps prevent
misunderstandings within the codebase.
