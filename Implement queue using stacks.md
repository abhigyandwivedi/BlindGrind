# Solution to "232. Implement Queue using Stacks"

## Problem Statement

Implement a first-in, first-out (FIFO) queue using two stacks. The queue should support the following operations:

- `push(x)`: Pushes element `x` to the back of the queue.
- `pop()`: Removes the element from the front of the queue.
- `peek()`: Gets the front element.
- `empty()`: Returns whether the queue is empty.

Example:

```
Input:
MyQueue queue = new MyQueue();
queue.push(1);
queue.push(2);
print(queue.peek());  // returns 1
print(queue.pop());   // returns 1
print(queue.empty()); // returns False
```

---

## Approach: Using Two Stacks

### Explanation

1. **Two Stacks:** Use two stacks, `input_stack` for enqueue operations and `output_stack` for dequeue operations.
2. **Push Operation:** Always push new elements onto `input_stack`.
3. **Pop/Peek Operation:** If `output_stack` is empty, move all elements from `input_stack` to `output_stack` to reverse the order.
4. **Empty Operation:** Both stacks must be empty for the queue to be empty.

---

## Implementation in Python

```python
class MyQueue:
    def __init__(self):
        self.input_stack = []
        self.output_stack = []

    def push(self, x: int) -> None:
        self.input_stack.append(x)

    def pop(self) -> int:
        self.peek()
        return self.output_stack.pop()

    def peek(self) -> int:
        if not self.output_stack:
            while self.input_stack:
                self.output_stack.append(self.input_stack.pop())
        return self.output_stack[-1]

    def empty(self) -> bool:
        return not self.input_stack and not self.output_stack

# Example usage
# queue = MyQueue()
# queue.push(1)
# queue.push(2)
# print(queue.peek())  # Output: 1
# print(queue.pop())   # Output: 1
# print(queue.empty()) # Output: False
```

---

## Complexity Analysis

1. **Time Complexity:**
    - `push(x)`: `O(1)` per push operation.
    - `pop()`: Amortized `O(1)` because each element is moved from `input_stack` to `output_stack` once.
    - `peek()`: Amortized `O(1)` for the same reason.
    - `empty()`: `O(1)`.
2. **Space Complexity:** `O(n)` for storing `n` elements across the two stacks.

---

## Example Run

Input:

```
push(1)
push(2)
peek() -> 1
pop() -> 1
empty() -> False
```

Output:

```
1
1
False
```

---

## Edge Cases

1. Popping from an empty queue → Should handle gracefully without errors.
2. Only one element in queue → Peek and pop should return that element.
3. Multiple elements pushed and popped → Should maintain FIFO order.

---

## Conclusion

This solution efficiently implements a queue using two stacks, ensuring FIFO operations with amortized constant time complexity.