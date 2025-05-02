# Understanding the `enum` Keyword in Rust

In Rust, the `enum` keyword is used to define **enumerations**. An enumeration (enum) is a type that can represent one of several possible values. Enums are often used to express a value that could be one of a set of predefined possibilities, making code more expressive and less error-prone.

---

## 🔧 Basic Syntax

```rust
enum EnumName {
    Variant1,
    Variant2,
    Variant3,
}
```

- `enum`: Declares the enumeration.
- `EnumName`: The name of the enum type.
- `Variant1`, `Variant2`, `Variant3`: The possible variants of the enum.

---

## 🧪 Example: Basic Enum

```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

fn main() {
    let move_direction = Direction::Up;

    match move_direction {
        Direction::Up => println!("Moving Up"),
        Direction::Down => println!("Moving Down"),
        Direction::Left => println!("Moving Left"),
        Direction::Right => println!("Moving Right"),
    }
}
```

> Output:
```
Moving Up
```

In this example, the `Direction` enum defines four possible values (`Up`, `Down`, `Left`, and `Right`), and we use a `match` statement to handle each variant.

---

## 📦 Enums with Data

Enums in Rust can also hold data in their variants, making them even more powerful.

### Example: Enum with Data

```rust
enum Shape {
    Circle(f64),      // Holds radius
    Rectangle(f64, f64), // Holds width and height
}

fn describe_shape(shape: Shape) {
    match shape {
        Shape::Circle(radius) => println!("Circle with radius: {}", radius),
        Shape::Rectangle(width, height) => println!("Rectangle with width {} and height {}", width, height),
    }
}

fn main() {
    let my_circle = Shape::Circle(10.0);
    let my_rectangle = Shape::Rectangle(5.0, 10.0);

    describe_shape(my_circle);
    describe_shape(my_rectangle);
}
```

> Output:
```
Circle with radius: 10
Rectangle with width 5 and height 10
```

In this example, the `Shape` enum contains variants that hold data (like `Circle` with a radius and `Rectangle` with width and height).

---

## 🔄 Enums with Multiple Data Types

Enums can even hold multiple types of data in different variants.

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
}

fn handle_message(msg: Message) {
    match msg {
        Message::Quit => println!("Quit message"),
        Message::Move { x, y } => println!("Move to ({}, {})", x, y),
        Message::Write(text) => println!("Writing: {}", text),
    }
}

fn main() {
    let move_msg = Message::Move { x: 10, y: 20 };
    let write_msg = Message::Write(String::from("Hello, World"));

    handle_message(move_msg);
    handle_message(write_msg);
}
```

> Output:
```
Move to (10, 20)
Writing: Hello, World
```

In this example, the `Message` enum has variants with named fields (`Move`) and a simple variant (`Quit`), as well as a variant that holds a `String`.

---

## 🚪 The `Option` and `Result` Enums

Rust has two common enums in the standard library:

- `Option`: Used for optional values (either `Some(T)` or `None`).
- `Result`: Used for functions that can return either a success (`Ok(T)`) or an error (`Err(E)`).

### Example: `Option` Enum

```rust
enum Option<T> {
    Some(T),
    None,
}

fn find_value(index: usize) -> Option<i32> {
    let values = vec![1, 2, 3];
    if index < values.len() {
        Option::Some(values[index])
    } else {
        Option::None
    }
}

fn main() {
    match find_value(1) {
        Option::Some(value) => println!("Found value: {}", value),
        Option::None => println!("Value not found"),
    }
}
```

> Output:
```
Found value: 2
```

---

## 🧳 Enum Pattern Matching

Rust enums are often used in conjunction with **pattern matching**. The `match` statement provides a powerful way to destructure and match against enum variants.

```rust
enum Animal {
    Dog(String),
    Cat(String),
    Bird(String),
}

fn make_sound(animal: Animal) {
    match animal {
        Animal::Dog(name) => println!("{} says woof", name),
        Animal::Cat(name) => println!("{} says meow", name),
        Animal::Bird(name) => println!("{} says chirp", name),
    }
}

fn main() {
    let my_dog = Animal::Dog(String::from("Buddy"));
    make_sound(my_dog);
}
```

> Output:
```
Buddy says woof
```

---

## 🧠 Summary

| Feature            | Description                                        |
|--------------------|----------------------------------------------------|
| `enum`             | Defines a type that can have several variants      |
| Data with Variants | Variants can hold different types of data          |
| Pattern Matching   | Commonly used with `match` to handle each variant  |
| `Option` & `Result`| Standard library enums for optional values & errors|

---

## ✅ When to Use `enum`

- When a value can be one of several options.
- To model a set of related data types (e.g., `Result` for error handling).
- When you need to work with variants that can hold additional data (like structs).

---

## 📚 Related Topics

- `match` keyword: For pattern matching against enum variants.
- `Option` and `Result` enums: Common enums in Rust's standard library.
- `struct` keyword: Can be used alongside enums for more complex data structures.

---

Let me know if you'd like further examples or explanations on other Rust keywords!
