# Understanding the `move` Keyword in Rust

Rust’s ownership system is a central part of the language’s memory safety guarantees. The `move` keyword is a powerful tool that explicitly **transfers ownership** of a captured variable into a **closure** or a **thread**, ensuring data is not accessed after it has been moved.

---

## 📦 What Does `move` Do?

The `move` keyword **forces a closure to take ownership** of the variables it captures from the environment, rather than borrowing them.

Normally, closures capture variables **by reference** if possible. Using `move` overrides this default behavior.

---

## 🔍 Syntax

```rust
let closure = move || {
    // use captured variables here
};
```

---

## 🧪 Example Without `move`

```rust
fn main() {
    let s = String::from("hello");

    let closure = || {
        println!("{}", s);
    };

    closure(); // works because `s` is borrowed, not moved
    println!("{}", s); // still accessible here
}
```

### ✅ Output:

```
hello
hello
```

Here, `s` is **borrowed** by the closure, so it can still be used afterward.

---

## 🧪 Example With `move`

```rust
fn main() {
    let s = String::from("hello");

    let closure = move || {
        println!("{}", s);
    };

    closure();
    // println!("{}", s); // ❌ Error: value borrowed here after move
}
```

### ❌ Compile Error (if `s` is accessed after closure)

This happens because `s` is **moved into the closure**. It no longer belongs to the outer scope.

---

## 🧵 Using `move` with Threads

```rust
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || {
        println!("Vector in thread: {:?}", v);
    });

    // println!("{:?}", v); // ❌ Error: `v` was moved
    handle.join().unwrap();
}
```

### ✅ Output:

```
Vector in thread: [1, 2, 3]
```

The `move` keyword is **required** here to transfer ownership into the thread. Without `move`, the closure would try to borrow `v`, which is not allowed across threads.

---

## 🧠 Summary

| Behavior     | Without `move`       | With `move`               |
|--------------|----------------------|----------------------------|
| Variable capture | By reference (borrow) | By value (ownership moved) |
| Ownership   | Retained in outer scope | Transferred to closure     |
| Usage after | Allowed               | Not allowed                |

---

## ✅ When to Use `move`

- When **transferring ownership** to a thread or closure.
- When you need to **extend the lifetime** of a variable inside a closure.
- When borrowing is not possible or causes lifetime errors.

---

## 📚 Related Concepts

- Ownership and Borrowing
- Closures
- Threads and Concurrency
- `Fn`, `FnMut`, `FnOnce` traits
