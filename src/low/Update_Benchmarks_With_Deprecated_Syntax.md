# Update Benchmarks With Deprecated Syntax

**Severity**: <span style="color:green;">Low</span>

## Description

Using deprecated syntax for defining benchmarks can lead to compatibility issues with future updates and may lack
support for newer features. Transitioning to the latest syntax enhances readability, maintainability, and compatibility
with the latest Substrate tooling.

## What should be avoided

```rust
benchmarks! {
	do_something {
        // Pre-benchmarking setup
        // ...
	}: _(RawOrigin::Signed(caller), data)
	verify {
        // Post-execution verifications
		// ...
	}
```

In this example:

- The benchmark setup and verification steps are embedded directly within the benchmarks! macro, which is now deprecated
  in favor of more modular and explicit syntax.

## Best practice

Use the new `#[benchmarks]` module syntax to define benchmarks in a more modular and explicit way. This structure
improves code organization by separating each benchmark into its own function with a more comprehensive syntax.

```rust
#[benchmarks]
mod benchmarks {
	use super::*;

	#[benchmark]
	fn do_something() {
        // Pre-benchmarking setup
        // ...

        // execute benchmark
		#[extrinsic_call]
		_(RawOrigin::Signed(caller), data);

        // Post execution verifications
        // ...
	}
```
