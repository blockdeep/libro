# Keep Dependencies Up to Date

**Severity**: High

## Description

Using outdated libraries can introduce security vulnerabilities, compatibility issues, and reduced performance, as older
dependencies may lack recent bug fixes and security patches.

## Avoid this

### Example 1:

The following code relies on an outdated library that may contain deprecated or insecure functions:

```rust
use outdated_library::deprecated_fn;
```

### Example 2:

The following code relies on an outdated library that may contain deprecated or insecure functions:

```toml
# In Cargo.toml
sp-runtime = { git = "https://github.com/paritytech/substrate.git", branch = "polkadot-v1.0.0" }
```

## Best Practice

Regularly update dependencies to their latest stable versions, ensuring the use of secure and well-maintained functions:

### Example 1:

```rust
use latest_library::safe_fn;
```

### Example 2:

The following code relies on an outdated library that may contain deprecated or insecure functions:

```toml
# In Cargo.toml
sp-runtime = { git = "https://github.com/paritytech/substrate.git", branch = "polkadot-stable2407" }
```

By updating to the latest versions, you benefit from security improvements, performance enhancements, and better
compatibility, ensuring a more robust and secure application.
