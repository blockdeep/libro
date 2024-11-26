# Avoid Unwrap Usage Inside Runtime

**Severity**: <span style="color:red;">Critical</span>

## Description

Using `unwrap()` and similar methods for error handling in Substrate runtime development can lead to runtime panics, which are particularly dangerous in a decentralized network. Such panics can cause block production to halt, disrupt the network, and compromise the reliability of the blockchain. Explicit error handling ensures more robust and predictable behavior, safeguarding the system against unexpected conditions in production environments.

## What should be avoided

The following example demonstrates how using `unwrap()` for error handling can result in runtime panics, which are neither user-friendly nor safe in a blockchain context:

```rust
// Create an empty vector: [ ]
let my_data = Vec::<u32>::new();

// Potential panic if index 0 is empty
let value = my_data.get(0).unwrap();

// Same error, with implicit unwrapping
let value = my_data[0];
```

In a Substrate runtime, such panics could stop block production, making the entire chain unrecoverable or in the best case provoking downtimes.

## Best practice

Handle errors explicitly by using `Result` and provide descriptive error messages:

```rust
#[pallet::error]
pub enum Error<T> {
	// Custom error
	MyError,
}

let my_data = Vec::<u32>::new();

// Gracefully handling the error
let value = my_data.get(0).ok_or(Error::<T>::MyError)?;
```

In this example:

- The code safely handles the case where `my_data.get(0)` might be `None`, allowing for graceful error handling and reducing the risk of panics.
