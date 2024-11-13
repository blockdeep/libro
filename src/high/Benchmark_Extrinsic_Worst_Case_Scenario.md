# Benchmark Extrinsic Worst-case Scenario

**Severity**: <span style="color:orange;">High</span>

## Description

Benchmarks that only cover typical scenarios may underestimate execution weights, potentially leading to resource
overuse or transaction failures in real-world usage.

## What should be avoided

The following code benchmarks a typical scenario, which may not account for the heaviest possible execution path,
leading to underestimated weights:

### Example 1:

```rust
#[benchmark]
fn typical_scenario() {
    // Benchmark with a small data set
    let items = generate_data(10);

    #[block]
    {
      process_items(items);
    }
}
```

In this example:

- The benchmark uses a small data set (`10` items), which may not reflect the workload in a worst-case scenario.

### Example 2:

```rust
#[pallet::call_index(0)]
#[pallet::weight(T::WeightInfo::some_extrinsic())]
pub fn some_extrinsic(origin: OriginFor<T>, input: bool) -> DispatchResult {
  let computation_result = match input {
    true  => 1,
    false => very_heavy_function(),
  };
  
  // Do something with the result.

  Ok(())
}

#[benchmark]
fn some_extrinsic() {
  let input = true;

  // Execution
  #[extrinsic_call]
  _(RawOrigin::Signed(account), input);
}
```

In this example:

- The worst path occurs when input is false, as this triggers the very_heavy_function() call. However, in the benchmark,
  input is set to true, meaning the benchmark will only measure the faster execution path. Consequently, the calculated
  execution cost will be an underestimate.

## Best practice

Benchmark at least the worst-case path by simulating the heaviest possible workload, ensuring the calculated weight
accurately reflects maximum resource usage:

### Example 1

```rust
#[benchmark]
fn worst_case_scenario(s: Linear<1, MAX_ITEMS>) {
    // Benchmark with dynamic data
    let items = generate_data(s);

    #[block]
    {
      process_items(items);
    }
}
```

In this improved example:

- `generate_data(s)` creates the maximum allowed data set to simulate a heavy load.
- By covering the worst-case path, this benchmark provides a realistic weight that prevents unexpected performance
  issues during peak loads.

### Example 2

```rust
#[benchmark]
fn some_extrinsic() {
  // Set the value to execute the worst-case path.
  let input = false;

  // Execution
  #[extrinsic_call]
  _(RawOrigin::Signed(account), input);
}
```

### Example 3

Alternatively, in mission-critical extrinsics that are meant to be used a lot, there could be a more fine-grained
approach, which is to benchmark each execution path independently:

```rust
#[pallet::call_index(0)]
#[pallet::weight(
     T::WeightInfo::some_extrinsic_path_1().max(
     T::WeightInfo::some_extrinsic_path_2())
)]
pub fn some_extrinsic(origin: OriginFor<T>, input: bool) -> DispatchResultWithPostInfo {
  let (result, weight) = match input {
    true  => (1, T::WeightInfo::some_extrinsic_path_1()),
    false => (very_heavy_function(), T::WeightInfo::some_extrinsic_path_2())
  };
  
  // Do something with the result.

  Ok(Some(weight).into())
}

#[benchmark]
fn some_extrinsic_path_1() {
  // Set the value to execute the path where the variable is true.
  let input = true;

  // Execution
  #[block]
  {
      some_extrinsic(RawOrigin::Signed(account), input);
  }
}

#[benchmark]
fn some_extrinsic_path_2() {
  // Set the value to execute the path where the variable is false.
  let input = false;

  // Execution
  #[block]
  {
      some_extrinsic(RawOrigin::Signed(account), input);
  }
}
```

In this example:

- The fee corresponding to the worst-case execution path will be initially taken from the user.
- However, not necessarily the worst-case execution path will be actually executed, and if the actual consumed fee is
  lower, the difference will be refunded to the user.
