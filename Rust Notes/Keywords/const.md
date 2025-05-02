# Understanding the `const` Keyword in Rust

The `const` keyword in Rust is used to define **constant values** that are available throughout the lifetime of the program. These constants are evaluated at compile time, ensuring their values are fixed and unchangeable.

---

## 🔧 Basic Syntax

```rust
const NAME: Type = value;
```

- `const` is the keyword used to declare a constant.
- `NAME` is the constant's name (conventionally uppercase).
- `Type` is the data type of the constant.
- `value` is the value assigned to the constant.

---

## 🧪 Example: Defining Constants

```rust
const PI: f64 = 3.14159265359;

fn main() {
    println!("Value of PI: {}", PI);
}
```

---

## 🧰 Constants and Type Annotations

When defining constants, you must explicitly annotate their type because the compiler can't infer it:

```rust
const MAX_SIZE: u32 = 100;
```

---

## 🚫 Constants are Immutable

Once a constant is defined, it cannot be changed. Attempting to modify a constant would result in a compile-time error:

```rust
const MAX_SIZE: u32 = 100;
MAX_SIZE = 200; // ❌ Error: cannot assign twice to immutable constant
```

---

## 🔒 Constants Are Evaluated at Compile Time

The values of constants are fixed at **compile time** and cannot change during runtime. This is different from variables, which can be assigned values during runtime.

```rust
const EARTH_RADIUS: u32 = 6371; // in kilometers
```

The value of `EARTH_RADIUS` is known at compile time and remains constant.

---

## 🧳 Constants Are Available Globally

Constants can be accessed anywhere within the scope of their visibility (just like static variables), and they are not tied to a particular instance like regular variables.

```rust
const GLOBAL_CONSTANT: i32 = 42;

fn print_constant() {
    println!("Global constant: {}", GLOBAL_CONSTANT);
}

fn main() {
    print_constant(); // Accessible globally
}
```

---

## 🧠 `const` vs. `static`

While both `const` and `static` allow the creation of globally available values, they have differences:

- `const` is for compile-time constants.
- `static` is used for values that are guaranteed to have a fixed memory location at runtime.

**`const` Example:**

```rust
const MAX_SIZE: u32 = 100;
```

**`static` Example:**

```rust
static HELLO: &str = "Hello, world!";
```

---

## ⚙️ Using `const` in Expressions

You can use constants in expressions, just like normal values:

```rust
const BASE: u32 = 10;
const HEIGHT: u32 = 20;
const AREA: u32 = BASE * HEIGHT;

fn main() {
    println!("Area: {}", AREA);
}
```

---

## 🚀 Constants and the `const fn` (Constant Functions)

Rust also supports **constant functions** (`const fn`), which allow you to perform computations at compile time.

```rust
const fn square(x: u32) -> u32 {
    x * x
}

const RESULT: u32 = square(5);

fn main() {
    println!("Square of 5 is: {}", RESULT);
}
```

In this example, the `square` function is evaluated at compile time, and the result is available as a constant.

---

## 🧠 Summary

| Feature                 | Description                          |
|-------------------------|--------------------------------------|
| `const`                 | Declares a compile-time constant     |
| Type Annotation         | Required when defining constants     |
| Immutable               | Constants cannot be modified         |
| Available Globally      | Constants are globally available     |
| `const fn`              | Allows computation at compile time   |

---

## ✅ When to Use `const`

- To define values that should never change (e.g., mathematical constants, configuration values).
- When you need to ensure a value is evaluated at compile time.
- When defining global constants used across functions.

---

## 📚 Related Topics

- `static` keyword: For fixed memory location values.
- `let` keyword: For declaring mutable variables.
- `const fn`: For compile-time functions.

---

Let me know if you'd like further examples or an explanation of other Rust keywords!
