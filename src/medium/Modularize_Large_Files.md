# Modularize Large Files

**Severity**: <span style="color:gold;">Medium</span>

## Description

In Substrate development, projects often contain a `lib.rs` file of a pallet or runtime configuration that is excessively large as it accumulates all logic, types, and configurations in one place. This is common in older templates but makes the codebase harder to navigate, understand, and maintain. Modern Substrate templates showcase best practices by modularizing `lib.rs` into smaller, purpose-specific modules, significantly improving code readability and scalability. Developers are encouraged to follow these newer conventions to align with contemporary standards and ensure their pallets are easier to maintain and extend.

## What should be avoided

A single large file with multiple unrelated functions and types can become hard to work with:

```rust
// lib.rs (single large file with all logic and types)
fn process_transaction() -> Result<Transaction, Error> { /* transaction processing logic */ }

fn calculate_fees() -> u32 { /* fee calculation logic */ }

fn validate_data() -> Result<(), Error> { /* data validation logic */ }

pub struct SomeStruct {
  // ...
}

pub type MyType = BoundedVec<u8, ConstU32<8>>;

pub enum UsefulEnum {
  // ...
}
```

In this example:

- All functionality and types is packed into one file, making it difficult to navigate and locate specific parts of the code.

## Best practice

Split the code into smaller, purpose-specific modules to improve organization and readability:

```rust
// ./lib.rs (main module file)
mod helpers;
mod types;

// --- ./helpers.rs ---
pub fn process_transaction() -> Result<Transaction, Error> { /* transaction processing logic */ }

pub fn calculate_fees() -> u32 { /* fee calculation logic */ }

pub fn validate_data() -> Result<(), Error> { /* data validation logic */ }

// --- ./types.rs ---
pub struct SomeStruct{
  // ...
}

pub type MyType = BoundedVec<u8, ConstU32<20>>;

pub enum UsefulEnum {
  // ...
}
```

In this modularized structure:

- Each module (`transaction.rs`, `fees.rs`, `validation.rs`) contains related functions, making the codebase more organized and easier to navigate.
- Developers can work on specific modules without wading through unrelated code, enhancing maintainability and team collaboration.
