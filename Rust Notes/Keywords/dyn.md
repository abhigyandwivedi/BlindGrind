
# Dyn
# Understanding the `dyn` Keyword in Rust

Rust is a statically typed language that emphasizes performance and safety. One of its features is **trait objects**, which allow for *dynamic dispatch*. The `dyn` keyword is used to define trait objects explicitly.

## What is `dyn`?

The `dyn` keyword in Rust is used to indicate **dynamic dispatch** for trait objects. It tells the compiler that you want to use a trait **at runtime**, rather than knowing the type at compile time.

This is useful when you want to write functions or structs that operate on *different types* implementing the same trait, but don't know exactly which types at compile time.

## Syntax

```rust
fn print_shape(shape: &dyn Shape) {
    shape.draw();
}
```

Here, `&dyn Shape` is a reference to a trait object. The actual type that implements `Shape` is not known at compile time, but the compiler ensures that `shape` implements `Shape`.

## Example: Using `dyn` for Polymorphism

```rust
trait Shape {
    fn draw(&self);
}

struct Circle;
struct Square;

impl Shape for Circle {
    fn draw(&self) {
        println!("Drawing a Circle");
    }
}

impl Shape for Square {
    fn draw(&self) {
        println!("Drawing a Square");
    }
}

fn print_shape(shape: &dyn Shape) {
    shape.draw();
}

fn main() {
    let circle = Circle;
    let square = Square;

    print_shape(&circle);
    print_shape(&square);
}
```

### Output

```
Drawing a Circle
Drawing a Square
```

## Why Use `dyn`?

- When you don’t know the concrete type ahead of time.
- To enable polymorphism across multiple types implementing the same trait.
- To reduce code duplication when using different types that share a behavior.

## Alternatives

If you know the type at compile time, you can use **generics** with **trait bounds** instead:

```rust
fn print_shape<T: Shape>(shape: &T) {
    shape.draw();
}
```

This uses **static dispatch** and can be more performant, but less flexible when working with heterogeneous collections of types.

## Conclusion

The `dyn` keyword is a powerful tool in Rust when dynamic behavior is needed. It trades off some compile-time performance and type-checking in favor of flexibility and runtime polymorphism.