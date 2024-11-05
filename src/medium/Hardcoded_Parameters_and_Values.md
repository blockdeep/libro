# Hardcoded Parameters and Values

**Severity**: Medium

## Description

Hardcoding parameters reduces flexibility, making the code less adaptable to different environments and configurations.
Configurable parameters allow for greater versatility and make the code easier to adjust as requirements change.

## What Should Not Be Done

Hardcoding values, such as limits or thresholds, can make it difficult to adapt the code without modifying the source:

```rust
// Hardcoded limit
const LIMIT: u32 = 100;
```

In this example:

- `LIMIT` is fixed at compile time, so changing it requires editing the code, recompiling, and redeploying, which can be
  inefficient.

## What can be done instead

Use configurable traits to allow parameter adjustments at the runtime level, enhancing flexibility and adaptability:

```rust
pub trait Config: frame_system::Config {
    const LIMIT: u32;
}

impl<T: Config> Pallet<T> {
    fn do_something() {
        // Access configurable limit
        let limit = T::LIMIT;
        // Logic that uses the configurable limit
    }
}
```

With this approach:

- `LIMIT` can be defined in the runtime configuration, allowing you to change it without modifying the source code.
- This setup makes the code adaptable to different environments and easily configurable to meet evolving needs.
