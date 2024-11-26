# Avoid Unrestricted XCM Execution

**Severity**: <span style="color:gold;">Medium</span>

## Description

It is not recommended to allow arbitrary users to send unrestricted instructions via XCM, especially given the presence of the `Transact` operation, which enables extrinsic execution through this method.

While standard security measures for extrinsics generally apply here, certain vulnerabilities may still arise.
Therefore, it is advisable to be as restrictive as possible unless a specific need justifies a more permissive approach, such as when the chain must regularly register assets on other chains.

## What should be avoided

The following code allows extrinsics with XCM instructions to pass unrestricted through `pallet-xcm`:

```rust
type XcmExecuteFilter = Everything;
```

This configuration enables all locations and instructions to execute XCM extrinsics without any filtering, creating a significant attack surface.

## Best practice

Restrict XCM execution to either no operations or to privileged users with clear justification. This limits the risk of exploitation and ensures that only authorized instructions are executed.

### Example 1

```rust
type XcmExecuteFilter = Nothing;
```

In this example:

- Setting the `XcmExecuteFilter` to `Nothing` disables the execution of extrinsics through XCM for all locations, ensuring a completely restricted environment.

### Example 2

```rust
pub struct CustomExecuteFilter;
impl<XcmCall> Contains<(Location, XcmCall)> for CustomExecuteFilter {
    fn contains(t: &(Location, XcmCall)) -> bool {
        let some_origin = SomeLocation::get();

        // Check if the origin location is the desired one.
        matches!(&t.0, some_origin)
    }
}

type XcmExecuteFilter = CustomExecuteFilter;
```

In this example:

- A custom filter, `CustomExecuteFilter`, is defined to enforce execution restrictions based on the origin location. Only instructions originating from the specified `SomeLocation` are permitted, ensuring tight control over which sources can execute extrinsics via XCM.

By applying these restrictions, the execution of XCM instructions is securely controlled, reducing the risk of misuse or unintended operations.
