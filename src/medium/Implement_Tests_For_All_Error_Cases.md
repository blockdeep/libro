# Implement Tests For All Error Cases

**Severity**: <span style="color:gold;">Medium</span>

## Description

Omitting tests for error cases in extrinsics can lead to unhandled scenarios and unexpected behavior in runtime
execution. By not verifying that specific errors are emitted when invalid conditions occur, important failure paths
remain untested, which can compromise the robustness of the code.

## What should be avoided

Avoid leaving out tests that validate the expected errors when certain invalid inputs or conditions are encountered.

```rust
// lib.rs
#[pallet::storage]
pub type ManagerAccount<T: Config> = StorageValue<_, T::AccountId>;

#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::do_something())]
pub fn do_something(origin: OriginFor<T>, input: u32) -> DispatchResult {
	let who = ensure_signed(origin)?;

    ensure!(who == ManagerAccount::<T>::get(), Error::<T>::UnexpectedAccount);
    ensure!(input > 0, Error::<T>::IncorrectInput);
    
    // Rest of the logic

    Ok(())
}

// tests.rs
#[test]
fn do_something_works() {
    let right_account = ManagerAccount::<Test>::get();
    let valid_input = 5;
    
    assert_ok!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        valid_input
    ));
}
```

In this example:

- The test only confirms that the function succeeds with valid inputs. It does not check whether appropriate errors are
  triggered when invalid accounts or inputs are provided.

## Best practice

Include tests that specifically verify all error cases the extrinsic is expected to handle. This ensures the extrinsic
behaves predictably even with incorrect inputs, making the system more robust and resilient.

```rust
#[test]
fn do_something_works() {
    let right_account = ManagerAccount::<Test>::get();
    let valid_input = 5;
     
    assert_ok!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        valid_input
    ));
}

#[test]
fn do_something_fails_if_wrong_account() {
    let wrong_account = get_wrong_account();
    let valid_input = 5;
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(wrong_account),
        valid_input
    ), Error::<Test>::UnexpectedAccount);
}

#[test]
fn do_something_fails_if_invalid_input() {
    let right_account = ManagerAccount::<Test>::get();
    let wrong_input = 0;
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        wrong_input
    ), Error::<Test>::IncorrectInput);
}
```
