# Lack of Interface Segregation

**Severity**: Medium

## Description

Overloading interfaces with too many responsibilities can lead to complex dependencies, making code harder to understand
and maintain.

## What should not be done

Using a single trait for multiple, unrelated responsibilities increases code complexity:

```rust
trait FullService {
    fn save();
    fn load();
    fn process();
}
```

## What can be done instead

Separate interfaces into smaller, focused traits to simplify code:

```rust
trait Save {
    fn save();
}

trait Load {
    fn load();
}

trait Process {
    fn process();
}
```

This approach keeps interfaces focused, improving code readability and maintainability.
