# Understanding the `for` Keyword in Rust

The `for` keyword in Rust is used to write **loops that iterate over items** in a collection or any type that implements the `IntoIterator` trait. It provides a safe and readable way to process sequences like arrays, vectors, ranges, and more.

---

## 🔧 Basic Syntax

```rust
for item in collection {
    // Use item
}
```

- `item` is a variable that takes on each value in `collection`.
- `collection` must implement the `IntoIterator` trait.

---

## 🧪 Example: Iterating Over a Range

```rust
fn main() {
    for i in 1..5 {
        println!("i = {}", i);
    }
}
```

> Output:
```
i = 1
i = 2
i = 3
i = 4
```

Note: The range `1..5` is exclusive of the end (`5`). Use `1..=5` to include `5`.

---

## 📦 Iterating Over a Vector

```rust
fn main() {
    let names = vec!["Alice", "Bob", "Charlie"];

    for name in names {
        println!("Hello, {}!", name);
    }
}
```

---

## 🔁 Iterating With Indexes (Using `.enumerate()`)

```rust
fn main() {
    let items = ["apple", "banana", "orange"];

    for (index, item) in items.iter().enumerate() {
        println!("{}: {}", index, item);
    }
}
```

> Output:
```
0: apple
1: banana
2: orange
```

---

## 🧰 Iterating Mutably With `iter_mut()`

```rust
fn main() {
    let mut numbers = [1, 2, 3];

    for num in numbers.iter_mut() {
        *num *= 2;
    }

    println!("Doubled: {:?}", numbers);
}
```

---

## ⚙️ Using `for` With `break` and `continue`

```rust
fn main() {
    for i in 0..10 {
        if i == 3 {
            continue; // Skip 3
        }
        if i == 6 {
            break; // Stop loop
        }
        println!("i = {}", i);
    }
}
```

---

## 🔄 Behind the Scenes: `IntoIterator`

The `for` loop uses the `IntoIterator` trait, which means:

```rust
for x in collection
```

is roughly equivalent to:

```rust
let mut iter = collection.into_iter();
while let Some(x) = iter.next() {
    // use x
}
```

---

## 🧠 Summary

| Component         | Description                              |
|------------------|------------------------------------------|
| `for`            | Loop over an iterator                    |
| `in`             | Separates loop variable from iterable    |
| `.iter()`        | Iterate by reference                     |
| `.iter_mut()`    | Iterate by mutable reference             |
| `.into_iter()`   | Consume and iterate                      |
| `break` / `continue` | Control flow in loops                |

---

## ✅ When to Use `for`

- When iterating over ranges, arrays, vectors, or collections
- When readability and safety are preferred
- When you need to avoid manual indexing

---

## 📚 Related Topics

- `while` and `loop` keywords
- Iterators and the `Iterator` trait
- `.map()`, `.filter()`, and `.collect()` for functional iteration

---

Let me know if you want to dive deeper into custom iterators or `for` with pattern matching!
