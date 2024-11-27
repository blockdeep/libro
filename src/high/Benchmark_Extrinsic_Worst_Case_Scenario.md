# Benchmark Extrinsic Worst-case Scenarios

**Severity**: <span style="color:orange;">High</span>

## Description

In Polkadot SDK, benchmarks are used to measure the computational cost of runtime operations, such as extrinsics, storage accesses, and logic execution. These costs are quantified in **weights**, which represent the time and resources required to execute a specific operation on the blockchain.

Through benchmarking, developers define the **`WeightInfo`** trait, which associates each extrinsic with a weight value based on the benchmarks. The runtime then uses these weights to enforce limits on block execution and calculate fees dynamically.

By performing benchmarks that account for worst-case scenarios, developers ensure their runtime remains efficient, secure, and scalable under real-world conditions. However, benchmarks that only cover typical scenarios may underestimate execution weights, potentially leading to resource overuse or transaction failures in real-world usage. To ensure accurate weight calculations, benchmarks must account for the heaviest possible execution path.

## What should be avoided

The following code benchmarks a typical scenario, which may not account for the heaviest possible execution path, leading to underestimated weights:

### Example 1

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

### Example 2

```rust
// ---- In pallet/lib.rs ----
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

// ---- In pallet/benchmarks.rs ----
#[benchmark]
fn some_extrinsic() {
  let input = true;

  // Execution
  #[extrinsic_call]
  _(RawOrigin::Signed(account), input);
}
```

In this example:

- The worst path occurs when input is false, as this triggers the `very_heavy_function` call. However, in the benchmark, input is set to true, meaning the benchmark will only measure the faster execution path. Consequently, the calculated execution cost will be an underestimate.

## Best practice

Benchmark at least the worst-case path by simulating the heaviest possible workload, ensuring the calculated weight accurately reflects maximum resource usage.

### Example 1

```rust
// ---- In pallet/benchmarks.rs ----
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
- By covering the worst-case path, this benchmark provides a realistic weight that prevents unexpected performance issues during peak loads.

### Example 2

```rust
// ---- In pallet/benchmarks.rs ----
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

For mission-critical extrinsics that are used frequently, consider benchmarking each execution path independently for finer weight granularity:

```rust
// ---- In pallet/lib.rs ----
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

// ---- In pallet/benchmarks.rs ----
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

- The fee corresponding to the worst-case execution path is initially charged to the user.
- If the actual execution consumes fewer resources than the worst-case scenario, the difference is refunded to the user.
