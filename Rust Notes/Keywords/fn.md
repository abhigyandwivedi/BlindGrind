# Understanding the `fn` Keyword in Rust

The `fn` keyword in Rust is used to **define functions**. Functions are reusable blocks of code that take input, perform operations, and optionally return a value.

---

## 🔧 Basic Syntax

```rust
fn function_name(parameter1: Type, parameter2: Type) -> ReturnType {
    // Function body
}
```

- `fn`: Declares a function
- `function_name`: The function's name
- Parameters are typed
- `-> ReturnType`: Optional; defines the return type
- The last expression (without `;`) is returned implicitly

---

## 🧪 Example: Simple Function

```rust
fn greet() {
    println!("Hello, world!");
}

fn main() {
    greet();
}
```

---

## 📥 Example: Function with Parameters

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b // Implicit return
}

fn main() {
    let result = add(5, 3);
    println!("5 + 3 = {}", result);
}
```

---

## ⚙️ Function with Explicit Return

```rust
fn multiply(x: i32, y: i32) -> i32 {
    return x * y; // Explicit return with semicolon
}
```

> Use `return` when early exit is needed or for clarity.

---

## 🧰 Function Without Return Type (Unit Type)

```rust
fn log_message(msg: &str) {
    println!("LOG: {}", msg);
}
```

If a function doesn’t return anything, it implicitly returns `()` (unit type).

---

## 🪜 Functions Can Call Other Functions

```rust
fn square(x: i32) -> i32 {
    x * x
}

fn sum_of_squares(a: i32, b: i32) -> i32 {
    square(a) + square(b)
}

fn main() {
    println!("Sum of squares: {}", sum_of_squares(3, 4));
}
```

---

## 🧬 Higher-Order Functions

Functions can take other functions as arguments:

```rust
fn apply<F>(f: F, x: i32) -> i32
where
    F: Fn(i32) -> i32,
{
    f(x)
}

fn main() {
    let result = apply(|x| x + 1, 5);
    println!("Result: {}", result);
}
```

---

## 🧠 Summary

| Keyword | Meaning                    |
|---------|----------------------------|
| `fn`    | Declares a function        |
| `-> T`  | Specifies return type `T`  |
| `()`    | Unit return type (no value)|
| `return`| Explicit return (optional) |

---

## ✅ When to Use `fn`

- To encapsulate logic into reusable components
- To break complex code into manageable parts
- To define entry points (like `main`)
- To pass behavior as arguments (`Fn` traits)

---

## 📚 Related Concepts

- Closures: `let add = |x, y| x + y;`
- Traits like `Fn`, `FnMut`, and `FnOnce`
- Function pointers: `fn(i32) -> i32`

---

Let me know if you’d like examples involving closures or recursive functions!
