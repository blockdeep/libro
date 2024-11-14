# Define Constants to Replace Magic Numbers

**Severity**: <span style="color:gold;">Medium</span>

## Description

Magic numbers (unexplained numeric constants) can make code hard to understand and maintain, as their purpose is often
unclear without comments or context.

## What should be avoided

Hardcoding numeric constants directly in the code makes their intent unclear:

```rust
// What does 7% represent?
let discount = price * Percent::from_percent(7);
```

## Best practice

Define constants with descriptive names to clarify their purpose and make code easier to read:

```rust
let discount_rate = Percent::from_percent(7);
let discount = price * discount_rate;
```

This approach improves readability and maintainability by making the purpose of constants explicit.
