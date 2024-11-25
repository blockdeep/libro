# Make Proper Usage of XCM `Junctions`

**Severity**: <span style="color:orange;">High</span>

## Description

`Junction`s are components within a `Location` that specify how to navigate through a chain of entities to reach a specific asset or resource.

However, due to their nature, some junctions are more explicit than others, which can lead to misuse — particularly with `GeneralIndex`, given its "generic" nature.

When defining junctions, adhere closely to their intended definitions to ensure they are used appropriately.

## What to avoid

Using `GeneralIndex`, or any other `Junction`, for purposes beyond representing the intended entity can result in misuse.

```rust
pub const AmountOfDecimals: u32 = 12;

pub const AssetOfZ: Location = Location::new(1, [Parachain(PARA_ID_OF_Z), GeneralIndex(AmountOfDecimals.into())]);
```

In this example, `GeneralIndex` is used to send information that describes a characteristic (the number of decimals) rather than the entity itself, which deviates from its intended purpose.

## Best practice

Use `Junctions` strictly to represent entities in the `Location` path, adhering to their intended definitions.

If parameters must be communicated via an XCM instruction and no existing field in the available instructions meets this purpose, an RFC should be opened [here](https://github.com/polkadot-fellows/RFCs/).
