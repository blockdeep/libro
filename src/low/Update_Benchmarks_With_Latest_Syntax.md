# Update Benchmarks With Latest Syntax

**Severity**: <span style="color:green;">Low</span>

## Description

Substrate's benchmarking system has evolved significantly between versions 1 and 2, with v2 introducing major improvements in flexibility, clarity, and modularity. In v1, the `benchmarks!` macro was used to define benchmarks in a less modular, more embedded format, making the code harder to maintain and update. The introduction of the `#[benchmarks]` attribute in v2 offers a cleaner, more organized approach. This new syntax separates setup, execution, and verification into distinct functions, improving code readability and making it easier to implement and update benchmarks as the Substrate framework evolves. Transitioning to v2 ensures compatibility with the latest tooling and enhances the overall development experience, providing a more robust foundation for performance testing in Substrate runtimes.

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

- The benchmark setup and verification steps are embedded directly within the benchmarks! macro, which is now deprecated in favor of more modular and explicit syntax.

## Best practice

Use the new `#[benchmarks]` attribute syntax to define benchmarks in a more modular and explicit way. This structure improves code organization by separating each benchmark into its own function with a more comprehensive syntax.

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
