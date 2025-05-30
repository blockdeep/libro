# Make Backend Logic Frontend-Agnostic

**Severity**: <span style="color:cyan;">Informational</span>

## Description

Backend logic should be independent of frontend-specific details, such as display formats, localization preferences, or user interface requirements, to ensure flexibility and consistency across different interfaces. By decoupling the backend from frontend concerns, developers can create a more maintainable and scalable system that can adapt to various frontend implementations without needing significant backend changes. This approach allows the backend to provide raw, unformatted data that can be tailored by the frontend to meet specific needs, promoting cleaner, more reusable code.

## What should be avoided

The following example ties backend logic to frontend-specific display preferences, which can cause inconsistencies and make the backend harder to adapt:

```rust
fn display_value() -> &str {
    let value = get_value();

    // Formats value with a frontend-specific currency display
    format!("${:.2}", value)
}
```

In this example:

- The function formats `value` in a currency-specific way, which may not be consistent with other frontends or
  localization requirements.

## Best practice

Keep backend functions agnostic to frontend requirements. Instead, return a raw value that can be formatted by the frontend as needed:

```rust
fn display_value_generic() -> u32 {
    let value = get_value();

    // Returns raw value without formatting
    value
}
```

In this approach:

- The backend returns a generic data type (e.g., `u32`), allowing frontend to format or display the value according to their own requirements.
- This separation keeps backend code adaptable and frontend-agnostic, making it easier to support diverse interfaces and localization needs.
