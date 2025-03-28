## Rust vs Go Iterators

Rust and Go handle iteration differently due to their distinct paradigms. Below is a comparison using the latest Go itertools additions.

---

## **Rust Iterators**

Rust provides powerful **lazy** iterators through the `Iterator` trait. They are efficient and allow method chaining without unnecessary allocations.

### **Key Features:**

- **Lazy Evaluation** - Iterators don’t execute until consumed.
    
- **Method Chaining** - Functional-style transformations (`map`, `filter`, `fold`, etc.).
    
- **Memory Efficiency** - No intermediate collections are created.
    
- **Custom Iterators** - Implement the `Iterator` trait for custom structs.
    

### **Example:**

```rust
fn main() {
    let nums = vec![1, 2, 3, 4, 5];

    let squared: Vec<i32> = nums.iter()
        .map(|x| x * x)
        .collect(); // Consumes the iterator

    println!("{:?}", squared); // Output: [1, 4, 9, 16, 25]
}
```

### **Custom Iterator Implementation:**

```rust
struct Counter {
    count: u32,
}

impl Counter {
    fn new() -> Counter {
        Counter { count: 0 }
    }
}

impl Iterator for Counter {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        self.count += 1;
        if self.count <= 5 {
            Some(self.count)
        } else {
            None
        }
    }
}

fn main() {
    let counter = Counter::new();
    for num in counter {
        println!("{}", num);
    }
}
```

---

## **Go Iterators (Using `slices` and Closures)**

Go 1.21 introduced the `slices` package, improving iteration and transformation functionalities.

### **Example: Iterating Over a Slice**

```go
package main

import (
    "fmt"
    "slices"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    squared := slices.Map(nums, func(x int) int {
        return x * x
    })

    fmt.Println(squared) // Output: [1, 4, 9, 16, 25]
}
```

### **Custom Iterator Using a Channel (Lazy Generator)**

```go
package main

import "fmt"

// Generator function using channels
func Counter(max int) <-chan int {
    ch := make(chan int)
    go func() {
        for i := 1; i <= max; i++ {
            ch <- i
        }
        close(ch)
    }()
    return ch
}

func main() {
    for num := range Counter(5) {
        fmt.Println(num)
    }
}
```

### **Custom Iterator with Closures**

```go
package main

import "fmt"

func Counter() func() (int, bool) {
    count := 0
    return func() (int, bool) {
        count++
        if count > 5 {
            return 0, false
        }
        return count, true
    }
}

func main() {
    next := Counter()
    for {
        num, ok := next()
        if !ok {
            break
        }
        fmt.Println(num)
    }
}
```

---

## **Comparison Table**

|Feature|Rust Iterators|Go Iterators (Using `slices`, Channels, Closures)|
|---|---|---|
|**Laziness**|Yes (Lazy by default)|No (Requires channels/closures)|
|**Method Chaining**|Yes (`map`, `filter`, `fold`)|Yes (`slices.Map()`)|
|**Custom Iterators**|`Iterator` trait (`next()`)|Channels, Closures|
|**Memory Efficiency**|High (zero-cost abstraction)|Moderate (channel overhead)|
|**Parallel Iteration**|Yes (`rayon` crate)|Yes (Goroutines + channels)|

---

## **Conclusion**

- **Rust iterators** are **powerful, built-in, and optimized** for **zero-cost abstraction**.
    
- **Go 1.21+ introduces `slices` utilities**, making iteration easier, but full iterator patterns still require **channels or closures**.
    

Would you like further examples or optimizations? 🚀