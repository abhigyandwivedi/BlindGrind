# Solution to "362. Design Hit Counter"

## Problem Statement

Design a hit counter that counts the number of hits received in the past 5 minutes (300 seconds).

Implement the `HitCounter` class:

1. `HitCounter()` initializes the object.
2. `void hit(int timestamp)` records a hit at the given `timestamp` (in seconds).
3. `int getHits(int timestamp)` returns the number of hits in the past 5 minutes.

Assume:

- `timestamp` is in non-decreasing order.
- Multiple hits can occur at the same `timestamp`.

---

## Approach: Queue-Based Solution

### Explanation

We can use a queue to store timestamps of hits.

1. **Hit Function:**
    
    - When a hit occurs, add the `timestamp` to the queue.
2. **Get Hits Function:**
    
    - Remove timestamps older than 300 seconds from the current `timestamp`.
    - The size of the queue represents the number of hits in the past 5 minutes.

### Example Walkthrough

For example, if the timestamps of hits are: `1, 2, 3, 300, 301`

- At `timestamp = 301`, remove hits at `1` (outside the 5-minute window).
- The queue will hold `[2, 3, 300, 301]`.
- The count of hits in the last 5 minutes is `4`.

---

## Implementation in Python

```python
from collections import deque

class HitCounter:
    def __init__(self):
        self.queue = deque()

    def hit(self, timestamp: int) -> None:
        self.queue.append(timestamp)

    def getHits(self, timestamp: int) -> int:
        while self.queue and self.queue[0] <= timestamp - 300:
            self.queue.popleft()
        return len(self.queue)
```

---

## Example Run

Input:

```python
counter = HitCounter()
counter.hit(1)
counter.hit(2)
counter.hit(3)
print(counter.getHits(4))    # Output: 3
counter.hit(300)
print(counter.getHits(300))  # Output: 4
print(counter.getHits(301))  # Output: 3
```

Output:

```
3
4
3
```

---

## Complexity Analysis

1. **Time Complexity:**
    
    - `hit(timestamp)`: `O(1)` - Append operation takes constant time.
    - `getHits(timestamp)`: `O(n)` - In the worst case, we remove all outdated hits.
2. **Space Complexity:** `O(n)`
    
    - The queue stores timestamps for up to `300` seconds.

---

## Edge Cases

1. If no hits occur, `getHits()` returns `0`.
2. If multiple hits occur at the same `timestamp`, all are counted.

---

## Conclusion

This queue-based approach provides an efficient solution for designing a hit counter, ensuring accurate hit counts within the specified time window.