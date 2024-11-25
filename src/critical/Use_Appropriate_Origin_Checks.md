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
protect critical functions.

### Example 1

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

In this example:

- Using `ensure_root` enforces that only users with root permissions can execute this function.

### Example 2

```rust
//Store an authorized account
#[pallet::storage]
pub type AuthorizedAccount<T: Config> = StorageValue<_, T::AccountId>;

impl<T: Config> Pallet<T> {
    pub fn ensure_authorized(origin: OriginFor<T>) -> Result<(), DispatchError> {
        let who: T::AccountId = ensure_signed(origin.clone())?;
        let authorized_origin: T::AccountId = Migrator::<T>::get();

        ensure!(sender == authorized_origin, Error::<T>::NotAuthorized);
        Ok(())
    }
}

#[pallet::call]
impl<T: Config> Pallet<T> {
    #[pallet::call_index(0)]
    #[pallet::weight(T::WeightInfo::execute_critical_operation())]
    pub fn execute_critical_operation(origin: OriginFor<T>) -> DispatchResult {
        // Restrict access to an authorized account
        Self::ensure_authorized(origin)?;

        // Secure function logic here
        execute_critical_operation();
    }
}
```

In this example:

- The pallet stores an Account under `AuthorizedAccount`, that is allowed to execute the permissioned extrinsic, the check is done though the `ensure_authorized()` function.
