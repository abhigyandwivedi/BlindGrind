# Understanding the `mut` Keyword in Rust

In Rust, variables are **immutable by default**. This means once a value is assigned to a variable, it cannot be changed. The `mut` keyword is used to make a variable **mutable**, allowing you to modify its value after it's been assigned.

---

## 🧠 What is `mut`?

The `mut` keyword is short for **mutable**, and it's used to declare variables whose values can change.

---

## 🔧 Basic Syntax

```rust
let mut variable_name = initial_value;
```

Without `mut`, attempting to change a variable after initialization results in a **compile-time error**.

---

## 🚫 Immutable by Default

```rust
fn main() {
    let x = 10;
    x = 20; // ❌ Error: cannot assign twice to immutable variable
}
```

### Error:
```
cannot assign twice to immutable variable `x`
```

---

## ✅ Correct Usage with `mut`

```rust
fn main() {
    let mut x = 10;
    println!("Before: {}", x);

    x = 20;
    println!("After: {}", x);
}
```

### Output:
```
Before: 10
After: 20
```

---

## 📦 Using `mut` with Struct Fields

```rust
struct Point {
    x: i32,
    y: i32,
}

fn main() {
    let mut p = Point { x: 1, y: 2 };
    p.x = 10; // OK because `p` is mutable
    println!("Point: ({}, {})", p.x, p.y);
}
```

---

## 🧩 `mut` in Pattern Matching

You can make a matched variable mutable using `mut` inside a `match` or `let` pattern:

```rust
fn main() {
    let (mut a, b) = (5, 10);
    a += 1;
    println!("a = {}, b = {}", a, b);
}
```

---

## 📚 `mut` in Function Parameters

```rust
fn increment(mut value: i32) {
    value += 1;
    println!("Incremented value: {}", value);
}

fn main() {
    increment(5); // value is copied and mutated locally
}
```

> Note: This doesn't mutate the original variable, only a copy of it.

---

## 🔁 `mut` in Loops

```rust
fn main() {
    let mut i = 0;
    while i < 3 {
        println!("i = {}", i);
        i += 1;
    }
}
```

---

## 🧪 Mutable References

When working with references, you also need to declare them as mutable:

```rust
fn main() {
    let mut s = String::from("hello");
    let r = &mut s; // mutable reference
    r.push_str(" world");
    println!("{}", r);
}
```

> Both the original binding and the reference must be mutable to change the value.

---

## ⚠️ Rules and Safety

- You must explicitly opt into mutability with `mut`.
- Only **one mutable reference** is allowed at a time to prevent data races.
- Rust enforces **safe concurrency** through these rules.

---

## 🧠 Summary

| Feature          | Description                                       |
|------------------|---------------------------------------------------|
| Immutable by default | Variables are not mutable unless declared with `mut`. |
| Function scope   | `mut` only applies within the scope it's declared. |
| Patterns         | Can be used with destructuring and pattern matching. |
| Safety           | Enforces strict rules to prevent unsafe mutations. |

---

## ✅ When to Use `mut`

- When a variable’s value needs to change.
- When working with loops or accumulators.
- When passing a mutable reference to a function for modification.

---

## 📚 Related Topics

- `let` keyword
- References and Borrowing (`&`, `&mut`)
- Ownership rules
- Shadowing vs Mutability

---

Let me know if you'd like explanations for more Rust keywords!
