# Understanding the `mod` Keyword in Rust

The `mod` keyword in Rust is used to **declare a module**. Modules help organize code into **logical units**, promote code reuse, and control visibility through the module system.

---

## 🧠 What Is a Module?

A module is a **namespace** that contains definitions for functions, structs, traits, constants, and other items. It allows you to break code into smaller, organized, and maintainable pieces.

---

## 🔧 Basic Syntax

```rust
mod my_module {
    pub fn greet() {
        println!("Hello from my_module!");
    }
}

fn main() {
    my_module::greet();
}
```

- `mod my_module {}` defines a module named `my_module`.
- You access public items from the module using `my_module::item`.

---

## 📂 Declaring Modules in Files

Rust allows modules to be declared in separate files using:

```rust
mod my_module;
```

Assuming a file named `my_module.rs` exists in the same directory, Rust will include it during compilation.

### File Layout Example

```
src/
├── main.rs
└── my_module.rs
```

**main.rs:**
```rust
mod my_module;

fn main() {
    my_module::say_hello();
}
```

**my_module.rs:**
```rust
pub fn say_hello() {
    println!("Hello from file-based module!");
}
```

---

## 📁 Submodules and Nested Modules

You can define modules inside other modules:

```rust
mod outer {
    pub mod inner {
        pub fn hello() {
            println!("Hello from inner!");
        }
    }
}

fn main() {
    outer::inner::hello();
}
```

---

## 🔐 Visibility with `mod`

By default, everything inside a module is private. Use `pub` to make it public:

```rust
mod math {
    pub fn add(a: i32, b: i32) -> i32 {
        a + b
    }

    fn hidden() {
        println!("You can't call this from outside!");
    }
}

fn main() {
    println!("2 + 3 = {}", math::add(2, 3));
    // math::hidden(); // ❌ Error: private function
}
```

---

## 🔄 Re-exporting with `pub use`

You can re-export items from a module to flatten the path:

```rust
mod tools {
    pub fn build() {
        println!("Building...");
    }
}

pub use tools::build;

fn main() {
    build(); // No need for tools::build
}
```

---

## 🧠 Summary

| Syntax              | Description                                         |
|---------------------|-----------------------------------------------------|
| `mod name {}`       | Defines an inline module                            |
| `mod name;`         | Declares a file-based module (`name.rs` or `name/mod.rs`) |
| `pub mod`           | Makes a module public                               |
| `pub fn`            | Makes a function inside a module accessible         |
| `mod` + `use`       | Common pattern to import and organize code          |

---

## ✅ When to Use `mod`

- To logically separate different parts of your program (e.g., `math`, `io`, `utils`)
- To organize large codebases
- To control visibility and encapsulation
- To create reusable components or libraries

---

## 📚 Related Topics

- `use` keyword (importing items)
- `pub`, `super`, `crate`, `self`
- File and module organization in Rust

---

Let me know if you'd like to see an example of a full project structure using modules!
