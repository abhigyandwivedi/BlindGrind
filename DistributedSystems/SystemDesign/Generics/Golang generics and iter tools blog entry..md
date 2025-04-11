
# Building a Generic Iterable with Comparator Support in Golang

## Introduction

Generics in Go (introduced in Go 1.18) allow us to write flexible, reusable code while maintaining type safety. In this post, we will build a **generic iterable with comparator support**, enabling us to:

1. Iterate over a collection with `HasNext()` and `Next()`.
    
2. Sort elements using a customizable comparator function.
    

This will be a step-by-step breakdown of how to create a robust iterable using Go generics.

---

## Understanding the Concept

Our implementation consists of:

- **Iterable Struct**: Holds a collection and provides iteration methods.
    
- **Comparator Function**: A function type for sorting elements.
    
- **Sorting Mechanism**: Uses Go’s built-in `slices.SortFunc` (Go 1.21+).
    

Now, let’s dive into the code!

---

## Step-by-Step Implementation

### **Step 1: Define the `Iterable` Struct**

```go
package main

import (
	"fmt"
	"slices"
)

// Iterable struct with generic type T
type Iterable[T any] struct {
	data []T
	pos  int
}
```

#### **Explanation:**

- `Iterable[T any]`: Declares a generic struct.
    
- `data []T`: Holds the collection of elements.
    
- `pos int`: Tracks the iteration position.
    

---

### **Step 2: Create an Iterable Constructor**

```go
// NewIterable creates a new iterable
func NewIterable[T any](data []T) *Iterable[T] {
	return &Iterable[T]{data: data, pos: 0}
}
```

#### **Explanation:**

- `NewIterable[T any]`: A generic constructor function.
    
- `data: data, pos: 0`: Initializes the iterable.
    

---

### **Step 3: Implement Iterator Functions**

```go
// HasNext checks if there are more elements
func (it *Iterable[T]) HasNext() bool {
	return it.pos < len(it.data)
}

// Next returns the next element
func (it *Iterable[T]) Next() T {
	if !it.HasNext() {
		var zero T
		return zero // Return zero value if exhausted
	}
	val := it.data[it.pos]
	it.pos++
	return val
}

// Reset resets the iterator position
func (it *Iterable[T]) Reset() {
	it.pos = 0
}
```

#### **Explanation:**

- `HasNext()`: Checks if more elements exist.
    
- `Next()`: Returns the next element and advances `pos`.
    
- `Reset()`: Resets iteration.
    

---

### **Step 4: Define a Generic Comparator**

```go
// Comparator function type
type Comparator[T any] func(a, b T) int
```

#### **Explanation:**

- `Comparator[T any]`: Function type that compares two values.
    
- Returns:
    
    - **Negative** if `a < b`.
        
    - **Positive** if `a > b`.
        
    - **Zero** if `a == b`.
        

---

### **Step 5: Implement Sorting**

```go
// Sort sorts the iterable using a custom comparator
func (it *Iterable[T]) Sort(cmp Comparator[T]) {
	slices.SortFunc(it.data, cmp)
	it.Reset() // Reset iterator after sorting
}
```

#### **Explanation:**

- `Sort(cmp Comparator[T])`: Sorts `data` using `slices.SortFunc`.
    
- `it.Reset()`: Resets iteration post sorting.
    

---

### **Step 6: Define Example Comparators**

```go
// Integer comparator
func IntComparator(a, b int) int {
	return a - b
}

// String comparator
func StringComparator(a, b string) int {
	if a < b {
		return -1
	} else if a > b {
		return 1
	}
	return 0
}
```

#### **Explanation:**

- `IntComparator()`: Orders integers.
    
- `StringComparator()`: Orders strings alphabetically.
    

---

### **Step 7: Putting It All Together**

```go
func main() {
	// Integer Iterable with Sorting
	ints := []int{5, 2, 8, 3, 1}
	intIterable := NewIterable(ints)

	fmt.Println("Before Sorting Integers:")
	for intIterable.HasNext() {
		fmt.Print(intIterable.Next(), " ")
	}

	// Sort the iterable
	intIterable.Sort(IntComparator)
	fmt.Println("\nAfter Sorting Integers:")
	for intIterable.HasNext() {
		fmt.Print(intIterable.Next(), " ")
	}
	fmt.Println()

	// String Iterable with Sorting
	strs := []string{"Banana", "Apple", "Cherry"}
	strIterable := NewIterable(strs)

	fmt.Println("\nBefore Sorting Strings:")
	for strIterable.HasNext() {
		fmt.Print(strIterable.Next(), " ")
	}

	// Sort the iterable
	strIterable.Sort(StringComparator)
	fmt.Println("\nAfter Sorting Strings:")
	for strIterable.HasNext() {
		fmt.Print(strIterable.Next(), " ")
	}
}
```

---

## **Expected Output**

```plaintext
Before Sorting Integers:
5 2 8 3 1 
After Sorting Integers:
1 2 3 5 8 

Before Sorting Strings:
Banana Apple Cherry 
After Sorting Strings:
Apple Banana Cherry 
```

---

## **Conclusion**

### **Key Takeaways:**

✅ Created a **generic iterable** with sequential access. ✅ Implemented a **comparator function** for sorting. ✅ Used **Go’s generics and slices.SortFunc** efficiently. ✅ Built a **flexible and reusable** utility for different data types.

🚀 With this, you can extend the iterable to support **filters, transformations, and additional iteration methods**!


```go
package main

import (
	"fmt"
	"slices"
)

// Iterable struct with generic type T
type Iterable[T any] struct {
	data []T
	pos  int
}

// NewIterable creates a new iterable
func NewIterable[T any](data []T) *Iterable[T] {
	return &Iterable[T]{data: data, pos: 0}
}

// HasNext checks if there are more elements
func (it *Iterable[T]) HasNext() bool {
	return it.pos < len(it.data)
}

// Next returns the next element
func (it *Iterable[T]) Next() T {
	if !it.HasNext() {
		var zero T
		return zero // Return zero value of T if no more elements
	}
	val := it.data[it.pos]
	it.pos++
	return val
}

// Reset resets the iterator position
func (it *Iterable[T]) Reset() {
	it.pos = 0
}

// Comparator function type
type Comparator[T any] func(a, b T) int

// Sort sorts the iterable using a custom comparator
func (it *Iterable[T]) Sort(cmp Comparator[T]) {
	slices.SortFunc(it.data, cmp)
	it.Reset() // Reset iterator after sorting
}

// Example integer comparator
func IntComparator(a, b int) int {
	return a - b
}

// Example string comparator
func StringComparator(a, b string) int {
	if a < b {
		return -1
	} else if a > b {
		return 1
	}
	return 0
}

func main() {
	// Integer Iterable with Sorting
	ints := []int{5, 2, 8, 3, 1}
	intIterable := NewIterable(ints)

	fmt.Println("Before Sorting Integers:")
	for intIterable.HasNext() {
		fmt.Print(intIterable.Next(), " ")
	}

	// Sort the iterable
	intIterable.Sort(IntComparator)
	fmt.Println("\nAfter Sorting Integers:")
	for intIterable.HasNext() {
		fmt.Print(intIterable.Next(), " ")
	}
	fmt.Println()

	// String Iterable with Sorting
	strs := []string{"Banana", "Apple", "Cherry"}
	strIterable := NewIterable(strs)

	fmt.Println("\nBefore Sorting Strings:")
	for strIterable.HasNext() {
		fmt.Print(strIterable.Next(), " ")
	}

	// Sort the iterable
	strIterable.Sort(StringComparator)
	fmt.Println("\nAfter Sorting Strings:")
	for strIterable.HasNext() {
		fmt.Print(strIterable.Next(), " ")
	}
}


```
