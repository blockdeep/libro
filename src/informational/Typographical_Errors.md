# Avoid Typographical Errors

**Severity**: Informational

## Description

Typographical errors in code or documentation can reduce professionalism, introduce potential bugs, and confuse readers
or contributors who rely on clear naming and consistent language.

## What should be avoided

Typographical errors can make code less readable and may even lead to bugs if used inconsistently:

```rust
// Typo in variable name
let amout_valu = 100;
```

In this example:

- The misspelled variable `amout_valu` is unclear and could lead to confusion, especially if referenced in multiple parts of
  the code.

## Best practice

Perform thorough proofreading to catch typos and enhance clarity, ensuring variable names and comments are accurate and
descriptive.

```rust
// Correctly spelled variable name
let amount_value = 100;
```

Using clear and correctly spelled names improves readability, maintains professionalism, and helps prevent
misunderstandings within the codebase.
