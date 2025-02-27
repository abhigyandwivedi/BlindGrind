# Solution to "295. Find Median from Data Stream"

## Problem Statement

The task is to design a data structure that supports the following operations efficiently:

1. **addNum(num):** Add an integer `num` from the data stream.
2. **findMedian():** Return the median of all elements so far.

Example:

```
Input:
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3)
findMedian() -> 2
```

---

## Approach: Two Heaps (Max-Heap and Min-Heap)

### Explanation

1. **Max-Heap:** Stores the smaller half of the numbers.
2. **Min-Heap:** Stores the larger half of the numbers.
3. **Balance Heaps:** Ensure the size difference between heaps is at most 1.
4. **Median Calculation:**
    - If both heaps are balanced, the median is the average of the two roots.
    - If one heap has more elements, its root is the median.

---

## Implementation in Python

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small = []  # Max-heap (inverted sign for Python min-heap)
        self.large = []  # Min-heap

    def addNum(self, num: int) -> None:
        heapq.heappush(self.small, -num)
        heapq.heappush(self.large, -heapq.heappop(self.small))

        if len(self.small) < len(self.large):
            heapq.heappush(self.small, -heapq.heappop(self.large))

    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2.0
```

---

## Example Run

Input:

```python
mf = MedianFinder()
mf.addNum(1)
mf.addNum(2)
print(mf.findMedian())  # Output: 1.5
mf.addNum(3)
print(mf.findMedian())  # Output: 2
```

Output:

```
1.5
2
```

---

## Complexity Analysis

1. **Time Complexity:**
    
    - `addNum`: `O(log N)` for heap insertion.
    - `findMedian`: `O(1)` as roots are accessed directly.
2. **Space Complexity:** `O(N)`
    
    - Storage for both heaps.

---

## Edge Cases

1. Single element → Median is that element.
2. Even number of elements → Median is the average of the middle two.

---

## Conclusion

The two-heap approach ensures efficient insertion and median retrieval, making it ideal for streaming data.