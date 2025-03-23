# Tough Generics Questions & Answers in Go

## 1. What are type parameters in Go generics, and how do they differ from regular function parameters?

**Answer:** Type parameters in Go generics allow defining functions, types, and methods that can operate on different types without specifying the exact type beforehand. Unlike regular function parameters, which hold values, type parameters define a placeholder type used inside the function or type definition.

Example:

```go
package main
import "fmt"

func PrintType[T any](value T) {
    fmt.Printf("%v is of type %T\n", value, value)
}

func main() {
    PrintType(42)       // Prints: 42 is of type int
    PrintType("hello")  // Prints: hello is of type string
}
```

---

## 2. What is a type constraint in Go generics? How is it defined?

**Answer:** A **type constraint** restricts the types that a generic function or struct can accept. It is defined using an interface.

Example using constraints:

```go
package main
import "fmt"

type Number interface {
    int | float64 | int64
}

func Sum[T Number](a, b T) T {
    return a + b
}

func main() {
    fmt.Println(Sum(3, 5))       // Works with int
    fmt.Println(Sum(3.2, 4.8))   // Works with float64
}
```

---

## 3. How do you define and use a generic function in Go? Provide an example.

**Answer:** A generic function in Go uses type parameters defined inside square brackets `[]`.

Example:

```go
package main
import "fmt"

func Identity[T any](value T) T {
    return value
}

func main() {
    fmt.Println(Identity(10))       // 10
    fmt.Println(Identity("Go"))    // Go
}
```

---

## 4. What are the limitations of Go generics compared to C++/Java?

**Answer:**

1. **No runtime type introspection** for generic types.
2. **Cannot use operators** (`+`, `-`, etc.) unless explicitly constrained.
3. **No variance or covariance** like in Java.
4. **Cannot create generic methods on non-generic types.**
5. **Cannot use reflection to manipulate generic types.**

---

## 5. Can you use multiple type parameters in a single generic function or struct?

**Answer:** Yes, you can define multiple type parameters.

Example:

```go
package main
import "fmt"

func Pair[T, U any](a T, b U) (T, U) {
    return a, b
}

func main() {
    fmt.Println(Pair(10, "hello"))
}
```

---

## 6. What is the role of `any` in Go generics? How does it relate to `interface{}`?

**Answer:** `any` is a built-in alias for `interface{}` and is used as a constraint to accept any type in generics.

```go
package main
import "fmt"

func Print[T any](value T) {
    fmt.Println(value)
}

func main() {
    Print("hello")
    Print(123)
}
```

---

## 7. How do Go generics improve performance compared to using interfaces?

**Answer:**

- Generics **avoid type assertions** and dynamic dispatch, leading to better performance.
- Generic functions are **statically compiled** for each concrete type, reducing runtime overhead.

---

## 8. Why can’t you use operators (like `+`, `-`, `*`) directly on generic types in Go?

**Answer:** Operators require concrete types that support them. A workaround is using constraints:

```go
package main
import "fmt"
import "golang.org/x/exp/constraints"

func Add[T constraints.Ordered](a, b T) T {
    return a + b
}

func main() {
    fmt.Println(Add(3, 5))
    fmt.Println(Add(2.5, 4.3))
}
```

---

## 9. What is the `constraints` package in Go, and how does it help with generics?

**Answer:** `constraints` provides pre-defined constraints like `constraints.Ordered` for types that support comparison operators.

---

## 10. How do generics impact type inference in Go? Can you provide an example where explicit type arguments are required?

**Answer:** Type inference works when function arguments determine the type. If ambiguity exists, explicit type arguments are needed.

```go
package main
import "fmt"

func Example[T any](value T) {
    fmt.Println(value)
}

func main() {
    Example[int](42)  // Explicit
    Example("text")    // Inferred
}
```

---

## Additional Advanced Questions on Go Generics

### 11. Write a generic function that finds the maximum element in a slice.

```go
package main
import "fmt"
import "golang.org/x/exp/constraints"

func Max[T constraints.Ordered](slice []T) T {
    max := slice[0]
    for _, v := range slice[1:] {
        if v > max {
            max = v
        }
    }
    return max
}

func main() {
    fmt.Println(Max([]int{3, 7, 2, 9, 5}))
    fmt.Println(Max([]float64{3.2, 7.1, 2.8, 9.5}))
}
```

### 12. Create a generic stack implementation using Go generics.

```go
package main
import "fmt"

type Stack[T any] struct {
    items []T
}

func (s *Stack[T]) Push(item T) {
    s.items = append(s.items, item)
}

func (s *Stack[T]) Pop() T {
    if len(s.items) == 0 {
        var zero T
        return zero
    }
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item
}

func main() {
    stack := Stack[int]{}
    stack.Push(10)
    stack.Push(20)
    fmt.Println(stack.Pop())
    fmt.Println(stack.Pop())
}
```

### 13. Implement a generic Map function that applies a transformation to each element of a slice.

```go
package main
import "fmt"

func Map[T any, U any](slice []T, transform func(T) U) []U {
    result := make([]U, len(slice))
    for i, v := range slice {
        result[i] = transform(v)
    }
    return result
}

func main() {
    nums := []int{1, 2, 3, 4}
    squared := Map(nums, func(x int) int { return x * x })
    fmt.Println(squared)
}
```

### 14. Write a generic function to swap two elements in a slice.

```go
package main
import "fmt"

func Swap[T any](slice []T, i, j int) {
    slice[i], slice[j] = slice[j], slice[i]
}

func main() {
    arr := []int{1, 2, 3, 4}
    Swap(arr, 1, 3)
    fmt.Println(arr)
}
```

### 15. Define a generic struct and show how to instantiate it with different types.

```go
package main
import "fmt"

type Container[T any] struct {
    value T
}

func main() {
    intContainer := Container[int]{42}
    stringContainer := Container[string]{"Hello"}
    fmt.Println(intContainer, stringContainer)
}
```

### 16. Write a function that takes a generic slice and returns a new slice with duplicate elements removed.

```go
package main
import "fmt"

func RemoveDuplicates[T comparable](slice []T) []T {
    seen := make(map[T]bool)
    result := []T{}
    for _, v := range slice {
        if !seen[v] {
            seen[v] = true
            result = append(result, v)
        }
    }
    return result
}

func main() {
    fmt.Println(RemoveDuplicates([]int{1, 2, 2, 3, 4, 4, 5}))
}
```

### 17. Implement a generic Reduce function that aggregates values from a slice.

```go
package main
import "fmt"

func Reduce[T any, U any](slice []T, reducer func(U, T) U, initial U) U {
    result := initial
    for _, v := range slice {
        result = reducer(result, v)
    }
    return result
}

func main() {
    nums := []int{1, 2, 3, 4}
    sum := Reduce(nums, func(acc, num int) int { return acc + num }, 0)
    fmt.Println(sum)
}
```

### 18. Can you create a method on a generic struct? Demonstrate with an example.

```go
package main
import "fmt"

type Box[T any] struct {
    value T
}

func (b Box[T]) Get() T {
    return b.value
}

func main() {
    b := Box[int]{10}
    fmt.Println(b.Get())
}
```

### 19. Write a generic function that merges two sorted slices of any comparable type.

```go
package main
import "fmt"

func Merge[T constraints.Ordered](a, b []T) []T {
    result := append(a, b...)
    return result
}

func main() {
    fmt.Println(Merge([]int{1, 3, 5}, []int{2, 4, 6}))
}
```

### 20. How would you implement a type-safe linked list using Go generics?

```go
package main
import "fmt"

type Node[T any] struct {
    value T
    next  *Node[T]
}

type LinkedList[T any] struct {
    head *Node[T]
}

func (l *LinkedList[T]) Append(value T) {
    newNode := &Node[T]{value: value}
    if l.head == nil {
        l.head = newNode
    } else {
        current := l.head
        for current.next != nil {
            current = current.next
        }
        current.next = newNode
    }
}

func main() {
    list := LinkedList[int]{}
    list.Append(10)
    list.Append(20)
    fmt.Println(list.head.value, list.head.next.value)
}
```

---
