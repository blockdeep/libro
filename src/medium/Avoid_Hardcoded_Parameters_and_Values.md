# Avoid Hardcoded Parameters and Values

**Severity**: <span style="color:gold;">Medium</span>

## Description

Hardcoding parameters reduces flexibility, making the code less adaptable to changing environments or configurations. In Substrate runtime development, this rigidity can lead to unnecessary re-deployments and upgrades when requirements change. Configurable parameters enhance versatility, allowing runtime adjustments without altering the source code.

A pallet configuration in Polkadot SDK is a set of associated types and constants defined in the `Config` trait of a pallet. These configurations allow developers to parameterize aspects of the pallet’s behavior, such as limits, thresholds, or external dependencies, at the runtime level. By implementing the `Config` trait in the runtime, these values can be adjusted dynamically for different environments without modifying or redeploying the pallet’s source code. This makes it an ideal replacement for hardcoded constants, providing flexibility and adaptability to evolving requirements.

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

- `LIMIT` is fixed at compile time, meaning any change requires editing the source code, recompiling, and redeploying the runtime. This process is inefficient and can disrupt the network.

## Best practice

Use configurable traits to allow parameter adjustments at the runtime level, enhancing flexibility and adaptability:

```rust
// --- In pallet/lib.rs file ---
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
