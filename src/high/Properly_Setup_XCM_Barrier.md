# Properly Setup XCM Barrier

**Severity**: High

## Description

As the name suggests, the `Barrier` type in the commonly used XCM executor serves as entry protection for execution on a
chain. It should be set explicitly to define which origins can execute without cost—such as for unbricking purposes—and
which should incur charges. Additionally, consider carefully which origins should be entirely restricted from access via
XCM.

As a rule of thumb, it is always recommended to be as restrictive as possible.

## What should be avoided

In the following example, there is a clear vulnerability: any origin can execute XCM for free on the chain using this
configuration

```rust
pub type Barrier = (
	xcm_builder::AllowUnpaidExecutionFrom<ThisParachain>,
	WithComputedOrigin<
		(AllowUnpaidExecutionFrom<ParentRelay>, AllowExplicitUnpaidExecutionFrom<Everything>),
		UniversalLocation,
		ConstU32<1>,
	>,
);
```

## Best Practice

Properly identify each relevant case, aiming to be as restrictive as possible while also requiring explicit
authorization for unpaid execution when necessary.

```rust
pub type Barrier = (
    // Allow XCMs with some computed origins to pass through.
    WithComputedOrigin<
        (
            // If the message is one that immediately attempts to pay for execution, then allow it.
            AllowTopLevelPaidExecutionFrom<OnlyTrustedChains>,
            // Parent, its pluralities (i.e. governance bodies), and the Fellows plurality
            // get free execution.
            AllowExplicitUnpaidExecutionFrom<ParentOrParentsExecutivePlurality>,
            // Subscriptions for version tracking are OK.
            AllowSubscriptionsFrom<ParentRelayOrSiblingParachains>,
        ),
        UniversalLocation,
        ConstU32<8>,
    >,
)
```

It is also highly recommended to support the configuration with inline comments that clarify the intended outcome.
