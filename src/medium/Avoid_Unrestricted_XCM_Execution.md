# Avoid Unrestricted XCM Execution

**Severity**: Medium

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

```rust
type XcmExecuteFilter = Nothing;
```
