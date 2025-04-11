

# Building a Generic Iterable with Comparator Support in Rust

## Introduction

Rust’s powerful generics and trait system enable us to create flexible, reusable abstractions. In this post, we will build a **generic iterable with comparator support**, allowing us to:

1. Iterate over a collection with `has_next()` and `next()`.
    
2. Sort elements using a customizable comparator function.
    

This will be a step-by-step breakdown of how to implement this in Rust.

---

## Understanding the Concept

Our implementation consists of:

- **Iterable Struct**: Holds a collection and provides iteration methods.
    
- **Comparator Function**: A function type for sorting elements.
    
- **Sorting Mechanism**: Uses Rust’s `sort_by()` method.
    

Now, let’s dive into the code!

---

## Step-by-Step Implementation

### **Step 1: Define the `Iterable` Struct**

```rust
struct Iterable<T> {
    data: Vec<T>,
    pos: usize,
}
```

#### **Explanation:**

- `Iterable<T>`: A generic struct that stores elements of type `T`.
    
- `data: Vec<T>`: Holds the collection.
    
- `pos: usize`: Tracks the iteration position.
    

---

### **Step 2: Implement an `Iterable` Constructor**

```rust
impl<T> Iterable<T> {
    fn new(data: Vec<T>) -> Self {
        Iterable { data, pos: 0 }
    }
}
```

#### **Explanation:**

- `new(data: Vec<T>) -> Self`: A constructor to create an `Iterable` instance.
    

---

### **Step 3: Implement Iterator Functions**

```rust
impl<T> Iterable<T> {
    fn has_next(&self) -> bool {
        self.pos < self.data.len()
    }

    fn next(&mut self) -> Option<&T> {
        if self.has_next() {
            let val = &self.data[self.pos];
            self.pos += 1;
            Some(val)
        } else {
            None
        }
    }

    fn reset(&mut self) {
        self.pos = 0;
    }
}
```

#### **Explanation:**

- `has_next()`: Checks if more elements exist.
    
- `next()`: Returns the next element and advances `pos`.
    
- `reset()`: Resets iteration.
    

---

### **Step 4: Define a Generic Comparator**

```rust
type Comparator<T> = fn(&T, &T) -> std::cmp::Ordering;
```

#### **Explanation:**

- `Comparator<T>`: Function type that compares two values.
    
- Returns:
    
    - `Ordering::Less` if `a < b`.
        
    - `Ordering::Greater` if `a > b`.
        
    - `Ordering::Equal` if `a == b`.
        

---

### **Step 5: Implement Sorting**

```rust
impl<T> Iterable<T> {
    fn sort(&mut self, cmp: Comparator<T>) {
        self.data.sort_by(cmp);
        self.reset(); // Reset iterator after sorting
    }
}
```

#### **Explanation:**

- `sort(cmp: Comparator<T>)`: Sorts `data` using `sort_by`.
    
- `self.reset()`: Resets iteration post sorting.
    

---

### **Step 6: Define Example Comparators**

```rust
use std::cmp::Ordering;

fn int_comparator(a: &i32, b: &i32) -> Ordering {
    a.cmp(b)
}

fn string_comparator(a: &String, b: &String) -> Ordering {
    a.cmp(b)
}
```

#### **Explanation:**

- `int_comparator()`: Orders integers.
    
- `string_comparator()`: Orders strings alphabetically.
    

---

### **Step 7: Putting It All Together**

```rust
fn main() {
    // Integer Iterable with Sorting
    let mut int_iterable = Iterable::new(vec![5, 2, 8, 3, 1]);

    println!("Before Sorting Integers:");
    while int_iterable.has_next() {
        println!("{}", int_iterable.next().unwrap());
    }

    int_iterable.sort(int_comparator);
    println!("\nAfter Sorting Integers:");
    while int_iterable.has_next() {
        println!("{}", int_iterable.next().unwrap());
    }

    // String Iterable with Sorting
    let mut str_iterable = Iterable::new(vec!["Banana".to_string(), "Apple".to_string(), "Cherry".to_string()]);

    println!("\nBefore Sorting Strings:");
    while str_iterable.has_next() {
        println!("{}", str_iterable.next().unwrap());
    }

    str_iterable.sort(string_comparator);
    println!("\nAfter Sorting Strings:");
    while str_iterable.has_next() {
        println!("{}", str_iterable.next().unwrap());
    }
}
```

---

## **Expected Output**

```plaintext
Before Sorting Integers:
5
2
8
3
1

After Sorting Integers:
1
2
3
5
8

Before Sorting Strings:
Banana
Apple
Cherry

After Sorting Strings:
Apple
Banana
Cherry
```

---

## **Conclusion**

### **Key Takeaways:**

✅ Created a **generic iterable** with sequential access. ✅ Implemented a **comparator function** for sorting. ✅ Used **Rust’s generics and sort_by** effectively. ✅ Built a **flexible and reusable** utility for different data types.

🚀 With this, you can extend the iterable to support **filters, transformations, and additional iteration methods**!