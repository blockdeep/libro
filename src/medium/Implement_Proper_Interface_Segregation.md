# Implement Proper Interface Segregation

**Severity**: <span style="color:gold;">Medium</span>

## Description

Overloading interfaces with too many responsibilities can create unnecessary complexity, making code harder to understand, test, and maintain. The Interface Segregation Principle (ISP) encourages the design of smaller, more focused interfaces that are easier to manage and modify.

## What should be avoided

Using a single interface (or trait) that encompasses multiple, unrelated responsibilities increases the complexity of the code and creates tight coupling.

```rust
trait FullService {
    fn save();
    fn load();
    fn process();
}
```

In this example:

- The FullService trait contains methods for unrelated operations (saving, loading, and processing), leading to unnecessary dependencies for any type that implements it.

## Best practice

Break down interfaces into smaller, focused traits to simplify code:

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
