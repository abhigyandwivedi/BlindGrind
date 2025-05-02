# Understanding the `struct` Keyword in Rust

The `struct` keyword in Rust is used to define custom data types that let you group together related data. A `struct` in Rust can be thought of as a composite data type that holds multiple pieces of data, potentially of different types, under a single name.

---

## 🧠 What is a `struct`?

A `struct` (short for structure) is a custom data type that allows you to store multiple pieces of data. Each piece of data inside a `struct` is called a **field**. Fields in a `struct` can have different types, and a `struct` provides a way to logically group them together.

---

## 🔧 Defining a Simple Struct

A basic `struct` definition consists of the `struct` keyword followed by a name and a list of fields with their respective types.

### Example: Basic `struct` Definition

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect = Rectangle {
        width: 30,
        height: 50,
    };

    println!("Width: {}, Height: {}", rect.width, rect.height); 
    // Output: Width: 30, Height: 50
}
```

### Explanation:
- `Rectangle` is the name of the `struct`.
- `width` and `height` are fields of the `struct` with types `u32`.
- In the `main` function, we create an instance of `Rectangle` by providing values for the fields.

---

## 🔧 Using `struct` to Encapsulate Data

`structs` are useful for encapsulating data. They allow you to create more complex data types by grouping primitive types together.

### Example: Using `struct` to Encapsulate Data

```rust
struct Person {
    name: String,
    age: u32,
}

fn main() {
    let person = Person {
        name: String::from("Alice"),
        age: 30,
    };

    println!("Name: {}, Age: {}", person.name, person.age); 
    // Output: Name: Alice, Age: 30
}
```

### Explanation:
- The `Person` `struct` encapsulates two fields: `name` (a `String`) and `age` (a `u32`).
- We create an instance of `Person` by providing values for the `name` and `age` fields.
- The `String::from` function is used to create a `String` from a string literal.

---

## 🔧 Struct with Methods

You can define methods on `struct`s using the `impl` (implementation) keyword. Methods allow you to define behavior that operates on instances of a `struct`.

### Example: Defining Methods on a Struct

```rust
struct Circle {
    radius: f64,
}

impl Circle {
    // Method to calculate area
    fn area(&self) -> f64 {
        std::f64::consts::PI * self.radius * self.radius
    }

    // Associated function (constructor)
    fn new(radius: f64) -> Self {
        Self { radius }
    }
}

fn main() {
    let circle = Circle::new(10.0);
    println!("Area of the circle: {}", circle.area()); 
    // Output: Area of the circle: 314.1592653589793
}
```

### Explanation:
- `Circle` is a `struct` with a single field `radius`.
- The `impl` block defines methods for `Circle`, including:
  - `area`: a method to calculate the area of the circle.
  - `new`: an associated function (constructor) to create a new `Circle` instance.
- We call the `area` method on an instance of `Circle` to calculate the area.

---

## 🔧 Tuple Structs

In addition to regular named fields, Rust allows you to define **tuple structs**, which are similar to tuples but named.

### Example: Tuple Struct Definition

```rust
struct Point(i32, i32);

fn main() {
    let point = Point(10, 20);
    println!("Point coordinates: ({}, {})", point.0, point.1); 
    // Output: Point coordinates: (10, 20)
}
```

### Explanation:
- `Point` is a tuple struct with two `i32` values.
- We create an instance of `Point` and access its fields using tuple indexing (`point.0`, `point.1`).

---

## 🔧 Structs with Option Types

Rust's `Option` type allows you to represent values that may or may not be present. You can use `Option` in `struct` fields to model data that may or may not be initialized.

### Example: Using `Option` in a Struct

```rust
struct Employee {
    name: String,
    job_title: Option<String>,
}

fn main() {
    let employee = Employee {
        name: String::from("Bob"),
        job_title: Some(String::from("Software Engineer")),
    };

    match &employee.job_title {
        Some(title) => println!("Job title: {}", title),
        None => println!("No job title assigned."),
    }
}
```

### Explanation:
- The `Employee` struct has a `job_title` field of type `Option<String>`, meaning the `job_title` might be present (wrapped in `Some`) or absent (wrapped in `None`).
- We use pattern matching to handle the `Option` type when accessing the `job_title` field.

---

## 🔧 Struct Update Syntax

Rust provides a shorthand syntax for updating fields of a `struct` based on an existing instance. This is known as **struct update syntax**.

### Example: Struct Update Syntax

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    // Creating a new Rectangle based on rect1
    let rect2 = Rectangle {
        width: 40,
        ..rect1 // Copies other fields from rect1
    };

    println!("Rectangle 2 - Width: {}, Height: {}", rect2.width, rect2.height);
    // Output: Rectangle 2 - Width: 40, Height: 50
}
```

### Explanation:
- The `..rect1` syntax copies the remaining fields from `rect1` when creating `rect2`. Only the `width` field is explicitly specified in `rect2`.

---

## 🧠 Summary

| Feature                | Description                                           |
|------------------------|-------------------------------------------------------|
| `struct`               | Defines a custom data type with named fields.         |
| Named Fields           | Fields in a `struct` are named and have explicit types.|
| Tuple Structs          | A shorthand for defining a `struct` with unnamed fields. |
| Methods                | Methods can be defined for `struct`s using `impl`.    |
| Associated Functions   | Functions tied to a `struct` that don’t take `self` as an argument. |
| Option Fields          | You can use `Option` to represent optional data.      |
| Struct Update Syntax   | A shorthand for creating a new `struct` by copying fields from an existing instance. |

---

## ✅ When to Use `struct`

- Use `struct` to define custom data types that group related data together.
- Use `structs` when you need to model real-world objects or concepts that have multiple attributes.
- Use `struct` to encapsulate data and define methods for interacting with that data.

---

## 📚 Related Concepts

- **Methods and Associated Functions** in Rust
- **Ownership and Borrowing** in Rust
- **Option and Result Types** in Rust
- **Pattern Matching** in Rust

---

Let me know if you'd like more examples or need clarification on any part of `struct` in Rust!
