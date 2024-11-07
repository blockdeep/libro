# Teleport Vs Reserve Transfer 

**Severity**: Critical

## Description

In a multi-consensus system environment where interconnections facilitate value transfers among participants, it’s essential to select the most effective asset transfer mechanism for integration with peers.

Currently, XCM and XCMP serve as solutions for such interactions. Given their 'fire-and-forget' nature, it’s crucial to understand the differences between teleporting assets and using the reserve asset transfer mechanism.

- Teleport: Assets are burned at the origin and minted at the destination, requiring full trust in issuance management between both parties.
- Reserve Transfer: Assets are deposited into a commonly trusted reserve, with a representative derivative minted at the destination. This approach allows both parties to rely on a globally trusted reserve, from which they can audit issuance.

The key distinction lies in trust: teleportation requires bilateral trust in issuance management, while reserve transfers depend on a single, globally trusted reserve for transparency and auditability.

## What should not be done

Accept teleports from multiple origins and set teleportation as the default method for sending and receiving tokens across other consensus systems.

These configurations can vary, but adjustments in xcm-executor require extreme caution. For instance, in an extreme scenario, we might allow all teleports; however, this caution also applies when selectively permitting specific teleports.

```rust
type IsTeleporter = Everything; 
```

## What can be done instead

Prioritize Reserve Asset transfers as the default token tranfer metho through consensus systems and use a trusted reserve such as Asset Hub. 

```rust
pub type Reserves = ReserveAssetsFrom<AssetReserveLocation>;
{...}
type IsReserve = Reserves;
```

In this example, only assets from a predefined reserve are accepted via Reserve Transfer. Adjust the level of permissiveness to suit your use case, and ensure sufficient time is spent making an informed decision.