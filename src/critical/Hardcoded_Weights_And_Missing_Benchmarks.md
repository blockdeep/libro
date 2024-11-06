# Hardcoded Weights and missing benchmarks

**Severity**: Critical

## Description

Hardcoding weights for extrinsics in a blockchain environment can lead to significant inaccuracies in resource
estimation. When weights are fixed, they may not reflect the actual execution costs or resource usage, resulting in
either overestimation or underestimation. This can adversely affect the performance of the blockchain, leading to
inefficient resource allocation and potentially causing failures under load.

## What should not be done

Avoid using hardcoded weights directly in the function definition of extrinsics.

```rust
#[pallet::call_index(0)]
#[pallet::weight(Weight::from_parts(10_000, 0) + T::DbWeight::get().reads_writes(1, 1))]
pub fn do_something(
    origin: OriginFor<T>,
    some_data: Data
) -> DispatchResult {...}
```

In this example:

- The weight is fixed, leading to potential inaccuracies in resource estimation, which can result in suboptimal
  performance and affect transaction processing on the network

## What can be done instead

Implement proper benchmarking to dynamically assess the weights of your functions. This process involves measuring the
actual execution costs during test runs and then applying the generated weights in your extrinsic definitions.

```rust
//benchmarking.rs file
#[benchmark]
fn do_something() {
    //setup
    ...
    //exection
	#[extrinsic_call]
	_(RawOrigin::Signed(account), data);
}

// Execute the benchmarks and then add the
// corresponding WeightInfo to the extrinsic
// inthe lib.rs file
#[pallet::call_index(0)]
#[pallet::weight(<T as Config>::WeightInfo::do_something())]
pub fn do_something(
    origin: OriginFor<T>,
    some_data: Data
) -> DispatchResult {...}
```
