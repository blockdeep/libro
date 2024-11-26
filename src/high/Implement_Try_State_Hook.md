# Implement `try-state` Hook

**Severity**: <span style="color:orange;">High</span>

## Description

In Substrate, **hooks** are specialized lifecycle methods that allow pallets to perform operations at specific points during the blockchain runtime's execution cycle. Common hooks include `on_initialize`, `on_finalize`, and `offchain_worker`, each serving a distinct purpose, such as initializing block-specific logic, finalizing block-level operations, or executing off-chain tasks.

The **`try-state` hook** is a specialized hook used exclusively during `try-runtime` builds. Unlike other hooks that are part of normal runtime operations, `try-state` is designed to validate storage state without altering it. This makes it an invaluable tool for debugging and testing, as it enables developers to simulate runtime upgrades, migrations, and other critical changes in a controlled environment.

The absence of `try-state` hooks prevents runtime sanity checks, making it harder to ensure that the storage state is sensible after upgrades or other critical operations. These hooks are executed only when the runtime is built with the `try-runtime` feature and provide a mechanism to validate state without altering storage, ensuring consistency and correctness. It is a best practice to run `try-runtime` prior to any migration to catch potential issues in a controlled environment.

## What should be avoided

Skipping sanity checks during runtime upgrades or migrations can leave storage inconsistencies unnoticed, leading to potential bugs:

```rust
fn on_runtime_upgrade() {
    // No validation of state consistency
    SomeStorage::<T>::mutate(|state| {
        *state = new_state;
    });
}
```

## Best practice

Implement the `try-state` hook to perform thorough state checks without altering storage. Use `try-runtime` to simulate migrations and validate state consistency before deploying updates:

```rust
#[pallet::hooks]
impl<T: Config> Hooks<BlockNumberFor<T>> for Pallet<T> {
    #[cfg(feature = "try-runtime")]
    fn try_state(_n: BlockNumber) -> Result<(), TryRuntimeError> {
        // Example: Ensure a storage map is non-empty.
        // No need to worry about weight consumption here.
        ensure!(!SomeStorage::<T>::iter().count().is_zero(), "Storage map is empty");

        // Add more sanity checks as needed.
        Ok(())
    }
}
```

The key benefits of this approach are:

1. **Controlled Validation**: The `try-state` hook ensures that the state is checked rigorously without altering storage, making it safe for runtime use.
2. **Integration with `try-runtime`**: When the node is built with the `try-runtime` feature, these hooks enable testing in a controlled environment, simulating runtime upgrades and migrations to catch potential issues early.
3. **Prevention of Errors**: Running `try-runtime` before deploying migrations reduces the risk of deploying a broken runtime, ensuring system stability.

By implementing `try-state` hooks and leveraging `try-runtime`, developers can validate and maintain storage consistency while catching potential issues early in the development cycle.
