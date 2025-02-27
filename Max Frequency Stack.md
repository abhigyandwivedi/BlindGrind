# Solution to "895. Maximum Frequency Stack"

## Problem Statement

Design a stack-like data structure that supports the following operations:

1. `push(int val)` - Pushes an integer `val` onto the stack.
2. `pop()` - Removes and returns the most frequent element in the stack.
    - If there is a tie, the element closest to the top of the stack is removed and returned.

---

## Approach: Hash Map + Stack

### Explanation

We use three data structures:

1. **Frequency Map:** Counts the occurrences of each value.
2. **Group Map:** Stores stacks of values grouped by frequency.
3. **Max Frequency:** Tracks the highest frequency.

### Algorithm Steps

1. **Push Operation:**
    
    - Increment the frequency of `val` in `freq`.
    - Push `val` into the corresponding frequency stack in `group`.
    - Update `maxFreq` if needed.
2. **Pop Operation:**
    
    - Pop the most frequent element from the stack corresponding to `maxFreq`.
    - Decrease its frequency in `freq`.
    - If the stack becomes empty, decrease `maxFreq`.

---

## Implementation in Python

```python
from collections import defaultdict

class FreqStack:
    def __init__(self):
        self.freq = defaultdict(int)
        self.group = defaultdict(list)
        self.maxFreq = 0

    def push(self, val: int) -> None:
        self.freq[val] += 1
        freq = self.freq[val]
        self.group[freq].append(val)
        self.maxFreq = max(self.maxFreq, freq)

    def pop(self) -> int:
        val = self.group[self.maxFreq].pop()
        self.freq[val] -= 1
        if not self.group[self.maxFreq]:
            self.maxFreq -= 1
        return val
```

---

## Example Run

Input:

```python
fs = FreqStack()
fs.push(5)
fs.push(7)
fs.push(5)
fs.push(7)
fs.push(4)
fs.push(5)

print(fs.pop())  # Output: 5
print(fs.pop())  # Output: 7
print(fs.pop())  # Output: 5
print(fs.pop())  # Output: 4
```

Output:

```
5
7
5
4
```

Explanation:

- `5` has the highest frequency (3 times).
- After popping `5`, `7` becomes the next most frequent.

---

## Complexity Analysis

1. **Time Complexity:**
    
    - `push`: `O(1)` — We update frequency and push to a stack.
    - `pop`: `O(1)` — We pop from the highest frequency stack.
2. **Space Complexity:** `O(n)`
    
    - Store frequency counts and grouped stacks.

---

## Edge Cases

1. Single element pushed multiple times → Pops in reverse order.
2. Multiple elements with the same frequency → Pops the most recent.

---

## Conclusion

This solution efficiently implements a frequency stack using hash maps and stacks, ensuring constant-time complexity for both push and pop operations.