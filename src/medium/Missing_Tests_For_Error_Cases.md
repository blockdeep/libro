# Missing tests for error cases

**Severity**: Medium

## Description

Omitting tests for error cases in extrinsics can lead to unhandled scenarios and unexpected behavior in runtime
execution. By not verifying that specific errors are emitted when invalid conditions occur, important failure paths
remain untested, which can compromise the robustness of the code.

## What should not be done

Avoid leaving out tests that validate the expected errors when certain invalid inputs or conditions are encountered.

```rust
#[pallet::call_index(1)]
pub fn do_something(origin: OriginFor<T>, inputs: Input) -> DispatchResult {
	let who = ensure_signed(origin)?;

    ensure!(who == SomeAccount::<T>::get(), Error::<T>::UnexpectedAccount)?;
    ensure!(inputs == expected_input, Error::<T>::IncorrectInput)?;

    Ok(())
}

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

## What can be done instead

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
fn fails_if_incorrect_account() {
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(wrong_account),
        expected_input
    ), Error::<Test>::UnexpectedAccount);
}

#[test]
fn fails_if_invalid_inputs() {
    assert_noop!(SomethingPallet::<Test>::do_something(
        RuntimeOrigin::signed(right_account),
        wrong_input
    ), Error::<Test>::IncorrectInput);
}
```
