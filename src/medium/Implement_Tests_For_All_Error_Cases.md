# Implement Tests For All Error Cases

**Severity**: Medium

## Description

Omitting tests for error cases in extrinsics can lead to unhandled scenarios and unexpected behavior in runtime
execution. By not verifying that specific errors are emitted when invalid conditions occur, important failure paths
remain untested, which can compromise the robustness of the code.

## What should be avoided

Avoid leaving out tests that validate the expected errors when certain invalid inputs or conditions are encountered.

```rust
// lib.rs
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::do_something())]
pub fn do_something(origin: OriginFor<T>, input: Input) -> DispatchResult {
	let who = ensure_signed(origin)?;

    ensure!(who == SomeAccount::<T>::get(), Error::<T>::UnexpectedAccount);
    ensure!(input == expected_input, Error::<T>::IncorrectInput);

    Ok(())
}

// tests.rs
#[test]
fn do_something_works() {
    assert_ok!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        expected_input
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
    assert_ok!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        expected_input
    ));
}

#[test]
fn do_something_fails_if_wrong_account() {
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(wrong_account),
        expected_input
    ), Error::<Test>::UnexpectedAccount);
}

#[test]
fn do_something_fails_if_invalid_input() {
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        wrong_input
    ), Error::<Test>::IncorrectInput);
}
```
