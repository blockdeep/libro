# Implement Proper Interface Segregation

**Severity**: <span style="color:gold;">Medium</span>

## Description

Overloading interfaces with too many responsibilities creates unnecessary complexity, making code harder to understand, test, and maintain. The [Interface Segregation Principle (ISP)](https://en.wikipedia.org/wiki/Interface_segregation_principle) advocates for designing smaller, more focused interfaces that are easier to manage and adapt. This principle ensures that implementing types are not burdened with methods they do not use, promoting modular and reusable code.

## What should be avoided

Using a single interface (or trait) that encompasses multiple, unrelated responsibilities increases complexity and creates tight coupling:

```rust
trait FullService {
    fn save();
    fn load();
    fn process();
}
```

In this example:

- The `FullService` trait combines unrelated methods for saving, loading, and processing. Any type implementing this trait would be forced to define all three methods, even if it only requires one or two of these responsibilities, leading to unnecessary dependencies.

## Best practice

Break down interfaces into smaller, focused traits to simplify code and improve modularity:

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

In this example:
- Distinct traits are implemented so that each component provides only the functionality it actually needs, thereby enhancing modularity and reducing coupling.
