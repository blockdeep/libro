# Define Constants to Replace Magic Numbers

**Severity**: <span style="color:gold;">Medium</span>

## Description

Magic numbers (unexplained numeric constants) make code difficult to understand and maintain because their purpose is often unclear without additional context or comments. In blockchain runtime development, where clarity is crucial to ensure correct behavior and security, such practices can lead to confusion, errors, or unintended consequences during updates or audits.

## What should be avoided

Hardcoding numeric constants directly in the code makes their intent unclear:

```rust
// What does 7% represent?
let discount = price * Percent::from_percent(7);
```

In this example:

- The meaning of `7` is ambiguous. Without context, other developers (or even the original author) may struggle to understand what it represents, increasing the risk of misinterpretation or misuse.

## Best practice

Define constants with descriptive names to clarify their purpose and make code easier to read:

```rust
const DISCOUNT_RATE: Percent = Percent::from_percent(7);

let discount = price * DISCOUNT_RATE;
```

This approach improves readability and maintainability by making the purpose of constants explicit.
