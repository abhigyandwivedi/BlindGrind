# Solution to "155. Min Stack"

## Problem Statement

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `push(int val)` pushes the element `val` onto the stack.
- `pop()` removes the element on the top of the stack.
- `top()` gets the top element.
- `getMin()` retrieves the minimum element in the stack.

Example:

```
Input:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   // Returns -3
minStack.pop();
minStack.top();      // Returns 0
minStack.getMin();   // Returns -2
```

---

## Approach: Using Two Stacks

### Explanation

1. **Main Stack:** Stores all elements as in a regular stack.
2. **Min Stack:** Stores the minimum value at each level of the stack.

When pushing an element, we also push the minimum of the current element and the previous minimum onto the `minStack`.

---

## Implementation in Python

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
        else:
            self.min_stack.append(self.min_stack[-1])

    def pop(self) -> None:
        if self.stack:
            self.stack.pop()
            self.min_stack.pop()

    def top(self) -> int:
        if self.stack:
            return self.stack[-1]
        return None

    def getMin(self) -> int:
        if self.min_stack:
            return self.min_stack[-1]
        return None

# Example usage
minStack = MinStack()
minStack.push(-2)
minStack.push(0)
minStack.push(-3)
print(minStack.getMin())  # Output: -3
minStack.pop()
print(minStack.top())      # Output: 0
print(minStack.getMin())   # Output: -2
```

---

## Example Run

Input:

```python
minStack = MinStack()
minStack.push(1)
minStack.push(2)
minStack.push(-1)
print(minStack.getMin())  # Output: -1
minStack.pop()
print(minStack.getMin())  # Output: 1
```

---

## Complexity Analysis

1. **Time Complexity:** `O(1)` for all operations (push, pop, top, getMin).
2. **Space Complexity:** `O(n)` for storing stack elements and corresponding min values.

---

## Edge Cases

1. Empty stack: `top()` and `getMin()` return `None` if the stack is empty.
2. Multiple minimum values: `min_stack` handles duplicate minimums correctly.

---

## Conclusion

This solution efficiently implements a Min Stack with constant-time operations for all required functionalities.