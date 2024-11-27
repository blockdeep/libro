# Make Proper Usage of XCM `Junctions`

**Severity**: <span style="color:orange;">High</span>

## Description

`Junction`s are components within a `Location` that specify how to navigate through a chain of entities to reach a specific asset or resource. In Substrate-based blockchains, `Junctions` are critical for ensuring clarity and precision in cross-consensus message (XCM) communications.

However, due to their flexible design, some junctions, such as `GeneralIndex`, are prone to misuse. Misusing these junctions can introduce ambiguity or inconsistency in the XCM message, potentially leading to integration issues, incorrect asset handling, or unintended behavior.

When defining `Junctions`, adhere closely to their intended definitions to maintain clarity and ensure proper usage.

## What to avoid

Using `GeneralIndex`, or any other `Junction`, for purposes beyond representing the intended entity can result in misuse and ambiguity.

```rust
pub const AmountOfDecimals: u32 = 12;

pub const AssetOfZ: Location = Location::new(1, [Parachain(PARA_ID_OF_Z), GeneralIndex(AmountOfDecimals.into())]);
```

In this example, `GeneralIndex` is used to send information that describes a characteristic (the number of decimals) rather than representing an actual entity in the path. This deviates from its intended purpose, creating potential confusion and misinterpretation of the XCM message.

## Best practice

Use `Junctions` strictly to represent entities in the `Location` path, adhering to their intended definitions. Avoid overloading their purpose to convey unrelated metadata or characteristics.

### Example

If the goal is to specify an asset within a parachain, use an appropriate `Junction`, such as `GeneralKey`, to represent the asset explicitly rather than overloading `GeneralIndex`.

```rust
pub const AssetOfZ: Location = Location::new(1, [Parachain(PARA_ID_OF_Z), GeneralKey(b"ZAssetKey".to_vec())]);
```

### Handling unmet requirements

If a scenario arises where existing `Junctions` or XCM instructions cannot meet the desired use case, avoid repurposing existing definitions. Instead, propose a new addition through the established governance process. Open an RFC [here](https://github.com/polkadot-fellows/RFCs/) to request new fields or instructions that align with the intended purpose.

By adhering to these guidelines, developers can ensure the integrity and clarity of XCM messages, preventing misuse and maintaining seamless interoperability between chains.
