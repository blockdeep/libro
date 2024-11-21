# Provide Event Documentation

**Severity**: <span style="color:gold;">Medium</span>

## Description

Events emitted by the runtime lack proper documentation, making it harder for users to understand their purpose. Additionally, Event documentation for each error provides valuable context inside the code metadata allowing frontend clients and users to get more insight regarding an event that is emitted.

## What should be avoided

Emitting events without descriptions or explanations:

```rust
#[pallet::event]
#[pallet::generate_deposit(pub(super) fn deposit_event)]
pub type Event<T: Config> {
    AccountCreated,
    AccountUpdated,
    AccountDeleted,
    AccountLocked,
}
```

In this example:

- No documentation is provided for the event variants inside the `Event` enum.

## Best practice

Provide detailed comments for each event to explain its purpose and usage:

```rust
#[pallet::event]
#[pallet::generate_deposit(pub(super) fn deposit_event)]
pub type Event<T: Config> {
    /// An account was just created. This event gets triggered when the account
    /// has a balance greater than the existential deposit for the first time.
    AccountCreated,
    /// The account got its balance updated, but over the existential deposit.
    AccountUpdated,
    /// The account got its balance under the existential deposit and its
    /// storage was completely wiped out.
    AccountDeleted,
    /// The account got blocked due to suspicious activities or misbehabiour.
    AccountLocked,
}
```
