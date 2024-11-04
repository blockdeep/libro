# Enforce Access Control to Protect Critical Functions

**Severity**: Critical

## Description

Leaving extrinsics open to all users without proper access control can allow unauthorized actions, potentially
compromising platform security and functionality.

## What should not be done

In the following code, the `execute` function can be called by any user, which may lead to unauthorized or malicious
actions:

```rust
pub fn execute() {
    // Function with unrestricted access
}
```

## What Can Be Done Instead

Implement access control checks to restrict function access to specific users or roles, such as administrators, to
protect critical functions.

```rust
pub fn execute(origin: OriginFor<T>) -> DispatchResult {
    ensure_root(origin)?; // Restrict access to the root (admin) user
    // Secure function logic here
}
```

Using `ensure_root` enforces that only users with root permissions can execute this function, reducing the risk of
unauthorized actions and enhancing security.
