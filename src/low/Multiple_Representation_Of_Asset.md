# Multiple Representation Of Asset

**Severity**: Low

## Description

The flexibility of Substrate and multi-consensus system environments can result in the same conceptual asset having multiple representations on a given chain. This should be addressed either by implementing a conversion system or, at the very least, by communicating this explicitly to the community to prevent misunderstandings and potential errors.

For example, on Asset Hub, tokens from Chain X bridged from Ethereum were registered under one AssetId, while tokens directly teleported from Chain X had a different AssetId, creating multiple representations of the same asset.

## What should be avoided

Generate these types of structures without explicitly acknowledging them.

## What can be done instead

Enable liquidity pools for 1:1 conversions, or clearly communicate the dual existence of assets. Any interacting user or integrating UI should have access to this information. Alternatively, design the tokenomics so that, while these tokens may coexist, users will naturally use only one of them once a specific point in the flow is reached.