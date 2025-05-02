# Understanding the `pub` Keyword in Rust

The `pub` keyword in Rust stands for **public** and is used to control the visibility of items such as functions, structs, modules, constants, and more. By default, everything in Rust is **private** to the current module. You must explicitly use `pub` to make something accessible from outside its defining scope.

---

## 🧠 Why `pub`?

Rust uses **module-based privacy**. If you want other modules or external crates to use your functions, types, or variables, you must declare them as `pub`.

---

## 🔧 Basic Usage

```rust
mod my_module {
    pub fn say_hello() {
        println!("Hello from my_module!");
    }
}
```

You can now call `say_hello` from outside `my_module`.

```rust
fn main() {
    my_module::say_hello();
}
```

Without `pub`, calling `my_module::say_hello()` would result in a compile-time error.

---

## 📦 Example: Public Struct and Field

```rust
mod my_structs {
    pub struct Person {
        pub name: String,
        pub age: u8,
    }
}
```

```rust
fn main() {
    let p = my_structs::Person {
        name: String::from("Alice"),
        age: 30,
    };
    println!("{} is {} years old.", p.name, p.age);
}
```

> If either the `Person` struct or its fields were not `pub`, this would not compile.

---

## 🚫 Private by Default

```rust
mod secret {
    fn whisper() {
        println!("This is a secret...");
    }
}

fn main() {
    // secret::whisper(); // ❌ Error: function is private
}
```

You must use `pub` to make `whisper` accessible from `main`.

---

## 🔍 `pub(crate)` — Crate-Only Visibility

This restricts visibility to the **current crate** only.

```rust
mod logger {
    pub(crate) fn log(msg: &str) {
        println!("Log: {}", msg);
    }
}
```

This function is visible **within the same crate**, but not from outside the crate.

---

## 🌐 `pub(super)` — Parent Module Only

```rust
mod outer {
    mod inner {
        pub(super) fn hello() {
            println!("Hello from inner");
        }
    }

    pub fn call_inner() {
        inner::hello(); // OK because of `pub(super)`
    }
}
```

---

## 🧰 Public Constants

```rust
pub const MAX_USERS: u32 = 100;
```

---

## 🎯 Public Enums

If an enum is `pub`, all its variants are automatically public:

```rust
pub enum Direction {
    North,
    South,
    East,
    West,
}
```

---

## 🧠 Summary

| Syntax               | Meaning                                |
|----------------------|----------------------------------------|
| `pub`                | Public (accessible everywhere)         |
| `pub(crate)`         | Accessible within the current crate    |
| `pub(super)`         | Accessible by the parent module        |
| _(default)_          | Private to current module              |

---

## ✅ When to Use `pub`

- When building libraries or APIs.
- When exposing types, functions, or constants across modules or crates.
- When defining struct fields or enum variants that must be used externally.

---

## 📚 Related Topics

- Modules and visibility in Rust
- `mod`, `crate`, and `super` keywords
- Encapsulation and API design

---

Let me know if you'd like similar guides for other Rust keywords!
