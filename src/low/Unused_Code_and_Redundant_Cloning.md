# Unused Code and Redundant Cloning

**Severity**: Low

## Description

Redundant code and cloning increase code size and decrease efficiency.

## What should not be done

```rust
let data = my_data.clone();
```

## What Can Be Done Instead

Remove unused code and optimize cloning operations.

```rust
let data = &my_data;
```


