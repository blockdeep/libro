# Use Safe Arithmetic Operations

**Severity**: <span style="color:orange;">High</span>

## Description

In Substrate runtime development, uncontrolled overflow or underflow is a critical issue because it can cause the chain to stall. Substrate’s deterministic execution model requires every node in the network to process transactions in the exact same way. If an unchecked arithmetic operation causes an overflow or underflow, the runtime will panic, leading to an unrecoverable state for the affected block.

## What should be avoided

The following code performs addition without checking for overflow, which may cause the program to wrap around to an unintended value:

```rust
// Potential for overflow if a + b exceeds the maximum value of the type.
let total: u16 = a + b;
```

In this example:

- If `a` and `b` are large, the result may exceed the data type’s maximum value, causing an overflow and leading to incorrect results.

## Best practice

### Option 1: Use Checked Arithmetic

Use `checked_add` to return an error if the operation exceeds the maximum value:

```rust
let total: u16 = a.checked_add(b).ok_or(Error::<T>::Overflow)?;
```

In this example:

- `checked_add` returns `None` if `a + b` would overflow, allowing us to handle the error with `ok_or`.
- This ensures that the operation will only proceed if the result is within bounds, preventing overflow-related issues.

### Option 2: Use Saturating Arithmetic

Alternatively, `saturating_add` ensures that the result will cap at the maximum value of the type rather than overflowing:

```rust
let total: u16 = a.saturating_add(b);
```

In this example:

- `saturating_add` will set `total` to the maximum possible value if `a + b` exceeds the type’s limit.
- This approach avoids panics or errors by safely capping the result, which is useful when an upper bound is acceptable in the application logic.

Both methods improve the reliability of arithmetic operations, ensuring predictable behavior without overflow.
