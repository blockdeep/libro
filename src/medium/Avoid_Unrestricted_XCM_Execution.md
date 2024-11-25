# Avoid Unrestricted XCM Execution

**Severity**: <span style="color:gold;">Medium</span>

## Description

It is not recommended to allow arbitrary users to send unrestricted instructions via XCM, especially given the presence
of the `Transact` operation, which enables extrinsic execution through this method.

While standard security measures for extrinsics generally apply here, certain vulnerabilities may still arise.
Therefore, it is advisable to be as restrictive as possible unless a specific need justifies a more permissive approach,
such as when the chain must regularly register assets on other chains.

## What should be avoided

The following code allows extrinsics with XCM instructions to pass through `pallet-xcm`.

```rust
type XcmExecuteFilter = Everything;
```

## Best practice

Ideally, no execution extrinsics should be allowed or should at least be restricted to privileged users unless there is
a clear justification for allowing them.

### Example 1

```rust
type XcmExecuteFilter = Nothing;
```

In this example:

- The `XcmExecuteFilter` is set to `Nothing`, effectively disabling the execution of extrinsics through XCM for all Locations.

### Example 2

```rust
pub struct CustomExecuteFilter;
impl <XcmCall> Contains<(Location, XcmCall)> for CustomExecuteFilter {
    fn contains(t: &(Location, XcmCall)) -> bool {
		let some_origin = SomeLocation::get();
		
        // Check if the origin location is the desired one.
        matches!(&t.0, some_origin)
    }
}

type XcmExecuteFilter = CustomExecuteFilter;
```

In this example:

- A custom filter, `CustomExecuteFilter`, is defined to enforce that extrinsics are executed only when the origin Location matches the configured location specified by `SomeLocation`.
