# Unused Code and Redundant Cloning

**Severity**: Low

## Description
Redundant code and cloning increase code size and decrease efficiency.

## Why It Should Not Be Done


```rust
let data = my_data.clone();
```



## What Can Be Done Instead



```rust
let data = &my_data;
```


