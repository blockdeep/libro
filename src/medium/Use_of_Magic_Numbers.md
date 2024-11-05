# Use of Magic Numbers

**Severity**: Medium

## Description

Magic numbers (unexplained numeric constants) can make code hard to understand and maintain, as their purpose is often
unclear without comments or context.

## What Should Not Be Done

Hardcoding numeric constants directly in the code makes their intent unclear:

```rust
let discount = price * Percent::from_percent(7); // What does 7% represent?
```

## What Can Be Done Instead

Define constants with descriptive names to clarify their purpose and make code easier to read:

```rust
let discount_rate = Percent::from_percent(7);
let discount = price * discount_rate;
```

This approach improves readability and maintainability by making the purpose of constants explicit.