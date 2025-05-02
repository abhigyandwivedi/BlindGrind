# Understanding the `union` Keyword in Rust

Rust provides the `union` keyword to define *union types*, which allow different fields to share the same memory. Unlike structs, unions are useful when you need to represent data that could take on several different, but mutually exclusive forms.

## What is a Union?

A `union` in Rust is a memory-efficient data structure where all fields occupy the same memory location. This means only one field is valid at a time. It’s an **unsafe feature** in Rust because it's up to the programmer to track which field is currently in use.

## Syntax

```rust
union MyUnion {
    i: i32,
    f: f32,
}
```

This declares a union named `MyUnion` with two fields: an integer `i` and a float `f`. Both share the same memory space.

## Example: Basic Usage

```rust
union IntOrFloat {
    i: i32,
    f: f32,
}

fn main() {
    let u = IntOrFloat { i: 42 };

    unsafe {
        println!("Union as integer: {}", u.i);
        // Accessing the float may yield unexpected results unless you know it was the last written value
        println!("Union as float: {}", u.f);
    }
}
```

### Output (example)

```
Union as integer: 42
Union as float: 5.885453e-44
```

## Why Use Unions?

- Memory efficiency when only one of several fields will be used at a time.
- Interfacing with low-level code, such as C APIs or embedded systems.
- Manual implementation of tagged unions or variant types.

## Important Notes

- You must use `unsafe` to read fields from a union.
- Unions don’t implement `Drop`, so they can’t contain fields that implement `Drop`.
- Unlike `enum`, unions don’t track which field is active.

## Example: FFI Interop

```rust
#[repr(C)]
union Value {
    int_val: i32,
    float_val: f32,
}

#[repr(C)]
struct MyData {
    tag: u8,
    value: Value,
}
```

This is a common pattern in FFI, where the `tag` helps determine how to interpret the contents of `value`.

## Conclusion

The `union` keyword in Rust offers low-level memory manipulation capabilities. While powerful, it must be used with caution due to safety concerns. Prefer `enum` for most cases where multiple types are needed, unless you have specific performance or FFI requirements.

---
