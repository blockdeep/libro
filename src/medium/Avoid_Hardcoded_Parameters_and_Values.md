# Avoid Hardcoded Parameters and Values

**Severity**: <span style="color:gold;">Medium</span>

## Description

Hardcoding parameters reduces flexibility, making the code less adaptable to different environments and configurations.
Configurable parameters allow for greater versatility and make the code easier to adjust as requirements change.

## What should be avoided

Hardcoding values, such as limits or thresholds, can make it difficult to adapt the code without modifying the source:

```rust
// Hardcoded limit
const LIMIT: u32 = 100;

impl<T: Config> Pallet<T> {
    fn do_something() {
        // No configurable limit
        for i in 0..T::LIMIT {
            // Logic that uses the configurable limit
        }
    }
}
```

In this example:

- `LIMIT` is fixed at compile time, so changing it requires editing the code, recompiling, and redeploying, which can be
  inefficient.

## Best practice

Use configurable traits to allow parameter adjustments at the runtime level, enhancing flexibility and adaptability:

```rust
// --- In pallet/lib.rs file ----
pub trait Config: frame_system::Config {
    const LIMIT: u32;
}

impl<T: Config> Pallet<T> {
    fn do_something() {
        // Access configurable limit
        for i in 0..T::LIMIT {
          // Logic that uses the configurable limit
        }
    }
}

// --- In runtime/lib.rs file ---
impl some_pallet::Config for Runtime {
    // ...
    type LIMIT = 100;
}
```

With this approach:

- `LIMIT` can be defined in the runtime configuration, allowing you to change it without modifying the source code.
- This setup makes the code adaptable to different environments and easily configurable to meet evolving needs.
