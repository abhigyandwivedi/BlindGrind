# Understanding the `continue` Keyword in Rust

In Rust, the `continue` keyword is used to **skip the current iteration** of a loop and proceed with the next iteration. It is most commonly used in `for`, `while`, and `loop` constructs to control the flow of iteration based on certain conditions.

---

## 🔧 Basic Syntax

```rust
continue;
```

- `continue` is used inside the body of a loop.
- It causes the loop to skip the current iteration and proceed with the next one.

---

## 🧪 Example: Skipping an Iteration in a `for` Loop

```rust
fn main() {
    for i in 1..6 {
        if i == 3 {
            continue; // Skip when i is 3
        }
        println!("i = {}", i);
    }
}
```

> Output:
```
i = 1
i = 2
i = 4
i = 5
```

In this example, the loop skips printing when `i` is equal to `3` and continues with the next iteration.

---

## 📦 Example: Skipping Odd Numbers

```rust
fn main() {
    for i in 1..10 {
        if i % 2 != 0 {
            continue; // Skip odd numbers
        }
        println!("Even number: {}", i);
    }
}
```

> Output:
```
Even number: 2
Even number: 4
Even number: 6
Even number: 8
```

Here, the loop skips the odd numbers and only prints even numbers.

---

## ⚙️ Using `continue` in a `while` Loop

```rust
fn main() {
    let mut count = 0;

    while count < 5 {
        count += 1;
        if count == 3 {
            continue; // Skip when count is 3
        }
        println!("Count: {}", count);
    }
}
```

> Output:
```
Count: 1
Count: 2
Count: 4
Count: 5
```

In this example, the `while` loop skips printing when `count` is equal to `3`.

---

## 🧰 Using `continue` in a `loop`

```rust
fn main() {
    let mut count = 0;

    loop {
        count += 1;

        if count == 3 {
            continue; // Skip when count is 3
        }

        if count > 5 {
            break; // Exit the loop
        }

        println!("Count: {}", count);
    }
}
```

> Output:
```
Count: 1
Count: 2
Count: 4
Count: 5
```

Here, `continue` causes the loop to skip the iteration when `count` is `3`, and the loop exits once `count` exceeds `5`.

---

## 🧠 Summary

| Feature            | Description                                |
|--------------------|--------------------------------------------|
| `continue`         | Skips the current iteration of a loop      |
| Can be used in     | `for`, `while`, and `loop` constructs      |
| Effect             | Causes the loop to immediately jump to the next iteration |
| Common Use Case    | Skipping iterations based on a condition   |

---

## ✅ When to Use `continue`

- When you need to skip specific iterations in a loop based on a condition.
- When you want to cleanly avoid unnecessary logic without using nested conditions.
- To improve the readability of the loop's flow control.

---

## 📚 Related Topics

- `break` keyword: Used to exit a loop completely.
- `for`, `while`, and `loop` keywords: Looping constructs in Rust.
- Conditional logic: Combining `if` statements with `continue` to control iteration.

---

Let me know if you'd like additional examples or explanations on other Rust keywords!
