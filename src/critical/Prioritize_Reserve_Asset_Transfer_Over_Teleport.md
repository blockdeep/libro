# Prioritize Reserve Asset Transfer Over Teleport

**Severity**: <span style="color:red;">Critical</span>

## Description

In a multi-consensus system environment where interconnections facilitate value transfers among participants, it is essential to select the most effective asset transfer mechanism for integration with peers.

Currently, XCM and XCMP serve as solutions for such interactions. Given their "fire-and-forget" nature, it is crucial to understand the differences between teleporting assets and using the reserve asset transfer mechanism:

- **Teleport**: Assets are burned at the origin and minted at the destination, requiring full trust in issuance management between both parties.
- **Reserve transfer**: Assets are deposited into a commonly trusted reserve, with a representative derivative minted at the destination. This approach allows both parties to rely on a globally trusted reserve, from which they can audit issuance.

The key distinction lies in trust: teleportation requires bilateral trust in issuance management, while reserve transfers depend on a single, globally trusted reserve for transparency and auditability.

## What should be avoided

Accepting teleports from multiple origins and setting teleportation as the default method for sending and receiving tokens across other consensus systems should be avoided.

These configurations can vary, but adjustments in `xcm-executor` require extreme caution. For instance, in an extreme scenario, allowing all teleports without restriction could lead to vulnerabilities; even selectively permitting specific teleports requires careful review.

```rust
type IsTeleporter = Everything;
```

## Recommended Configuration

Prioritize Reserve Asset transfers as the default token transfer method through consensus systems and use a trusted reserve such as `Asset Hub`.

```rust
pub type Reserves = ReserveAssetsFrom<AssetReserveLocation>;
// ...
type IsReserve = Reserves;
```

In this example, only assets from a predefined reserve are accepted via Reserve transfer. Adjust the level of permissiveness to suit your use case, and ensure sufficient time is spent making an informed decision.
