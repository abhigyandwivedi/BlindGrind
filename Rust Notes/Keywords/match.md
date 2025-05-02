# Understanding the `match` Keyword in Rust

The `match` keyword in Rust is a powerful control flow construct that allows pattern matching. It’s similar to `switch` statements in other languages but far more powerful and expressive.

---

## 🧠 What is `match`?

The `match` keyword allows you to compare a value against a series of patterns and execute code based on which pattern matches. Every possible value must be covered (either explicitly or using `_` for a catch-all).

---

## 🔧 Basic Syntax

```rust
match value {
    pattern1 => expression1,
    pattern2 => expression2,
    _ => default_expression,
}
```

- Each `pattern` is compared to the `value`.
- The arrow (`=>`) separates the pattern from the result/expression.
- The `_` acts as a wildcard (default case).
- The match arms must return the same type.

---

## 📦 Example: Matching Integers

```rust
fn main() {
    let number = 3;

    match number {
        1 => println!("One"),
        2 => println!("Two"),
        3 => println!("Three"),
        _ => println!("Other number"),
    }
}
```

### Output:
```
Three
```

---

## 🎯 Example: Matching with Ranges

```rust
fn main() {
    let age = 25;

    match age {
        0..=12 => println!("Child"),
        13..=19 => println!("Teenager"),
        20..=64 => println!("Adult"),
        _ => println!("Senior"),
    }
}
```

### Output:
```
Adult
```

- `0..=12` matches any value from 0 to 12, inclusive.

---

## 💡 Example: Matching Enums

```rust
enum Direction {
    North,
    South,
    East,
    West,
}

fn main() {
    let dir = Direction::North;

    match dir {
        Direction::North => println!("Going north!"),
        Direction::South => println!("Going south!"),
        Direction::East => println!("Going east!"),
        Direction::West => println!("Going west!"),
    }
}
```

### Output:
```
Going north!
```

---

## 🧩 Destructuring with `match`

```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let p = Point { x: 0, y: 7 };

    match p {
        Point { x: 0, y } => println!("Point on y-axis at {}", y),
        Point { x, y: 0 } => println!("Point on x-axis at {}", x),
        Point { x, y } => println!("Point at ({}, {})", x, y),
    }
}
```

### Output:
```
Point on y-axis at 7
```

---

## 🎛 Example: Returning Values from `match`

```rust
fn get_grade(score: u8) -> &'static str {
    match score {
        90..=100 => "A",
        80..=89 => "B",
        70..=79 => "C",
        60..=69 => "D",
        _ => "F",
    }
}

fn main() {
    let grade = get_grade(85);
    println!("Grade: {}", grade);
}
```

### Output:
```
Grade: B
```

- `match` can be used as an expression to return values directly.

---

## 🧠 Summary

| Feature                | Description                                                               |
|------------------------|---------------------------------------------------------------------------|
| Pattern Matching       | Compare a value to multiple patterns.                                     |
| Exhaustiveness         | All possibilities must be covered (`_` can be used as a catch-all).       |
| Expression Context     | `match` can return values and be used in variable bindings.               |
| Destructuring Support  | Works with structs, enums, tuples, and more.                              |

---

## ✅ When to Use `match`

- When you need exhaustive handling of all possible cases.
- When working with enums and pattern matching is necessary.
- When returning different values based on input conditions.
- As a cleaner alternative to nested `if`/`else` statements.

---

## 📚 Related Topics

- `if let` and `while let`
- `enum` and pattern matching
- Guards in match arms (`if` conditions)
- Destructuring in patterns

---

## 🔒 Bonus: Match Guards

```rust
fn main() {
    let num = Some(4);

    match num {
        Some(x) if x < 5 => println!("Less than five: {}", x),
        Some(x) => println!("Number: {}", x),
        None => println!("No number"),
    }
}
```

### Output:
```
Less than five: 4
```

- `if x < 5` is a **match guard** — an additional condition for a pattern.

---

Let me know if you’d like to learn about `if let`, `while let`, or match in combination with enums or error handling!
