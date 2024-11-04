# Avoid Typographical Errors to Maintain Professionalism and Clarity

**Severity**: Informational

## Description

Typographical errors in code or documentation can reduce professionalism, introduce potential bugs, and confuse readers
or contributors who rely on clear naming and consistent language.

## What Should Not Be Done

Typographical errors can make code less readable and may even lead to bugs if used inconsistently:

```rust
let amout = 100; // Typo in variable name
```

In this example:

- The misspelled variable `amout` is unclear and could lead to confusion, especially if referenced in multiple parts of
  the code.

## What can be done instead

Perform thorough proofreading to catch typos and enhance clarity, ensuring variable names and comments are accurate and
descriptive.

```rust
let amount = 100; // Correctly spelled variable name
```

Using clear and correctly spelled names improves readability, maintains professionalism, and helps prevent
misunderstandings within the codebase.
