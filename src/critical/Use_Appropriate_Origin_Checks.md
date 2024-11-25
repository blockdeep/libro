# Use Appropriate Origin Checks

**Severity**: <span style="color:red;">Critical</span>

## Description

Leaving extrinsics open to all users without proper origin checks can allow unauthorized actions, potentially
compromising security and functionality.

## What should be avoided

In the following code, the `execute` function can be called by any user, which may lead to unauthorized or malicious
actions:

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::execute_critical_operation())]
pub fn execute_critical_operation(origin: OriginFor<T>) -> DispatchResult {
    // Function with unrestricted access
    execute_critical_operation();
}
```

In this example

- The extrinsic can be executed by anyone because there are no access control checks in place, which can be particularly problematic for critical chain operations.

## Best practice

Implement appropriate origin checks to restrict function access to specific users or roles, such as elevated origins, to
protect<span style="color:red;">Critical</span> functions.

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::execute_critical_operation())]
pub fn execute_critical_operation(origin: OriginFor<T>) -> DispatchResult {
    // Restrict access to the root (admin) user
    ensure_root(origin)?;

    // Secure function logic here
    execute_critical_operation();
}
```

Using `ensure_root` enforces that only users with root permissions can execute this function, reducing the risk of
unauthorized actions and enhancing security.

You can also create your own origin checks by implementing custom origins. See an example here: **ADD example from Polkadot SDK code (GitHub link)**.
