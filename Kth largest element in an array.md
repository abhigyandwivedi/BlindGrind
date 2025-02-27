# Solution to "215. Kth Largest Element in an Array"

## Problem Statement

Given an integer array `nums` and an integer `k`, return the `k`th largest element in the array.

Note that it is the `k`th largest element in the sorted order, not the `k`th distinct element.

---

## Approach: Min-Heap

### Explanation

We can solve this problem efficiently using a **Min-Heap**. The idea is to maintain a heap of size `k` while iterating through the array.

### Algorithm Steps

1. Create a min-heap of size `k`.
2. Iterate through each element of `nums`:
    - Add the element to the heap.
    - If the heap size exceeds `k`, remove the smallest element.
3. The root of the heap will contain the `k`th largest element.

### Example Walkthrough

For example, given the input:

```
nums = [3, 2, 1, 5, 6, 4]
k = 2
```

1. Build a min-heap with the first `k` elements: `[3, 2]`.
    
2. Iterate through the rest of the array:
    
    - Add `1`: Heap remains `[3, 2]` (1 is smaller than the heap root).
    - Add `5`: Heap becomes `[3, 5]` (2 is removed).
    - Add `6`: Heap becomes `[5, 6]` (3 is removed).
    - Add `4`: Heap remains `[5, 6]` (4 is smaller than the root).
3. The root of the heap (`5`) is the `2`nd largest element.
    

---

## Implementation in Python

```python
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        min_heap = []

        for num in nums:
            heapq.heappush(min_heap, num)
            if len(min_heap) > k:
                heapq.heappop(min_heap)

        return min_heap[0]
```

---

## Example Run

Input:

```python
nums = [3, 2, 1, 5, 6, 4]
k = 2
solution = Solution()
print(solution.findKthLargest(nums, k))
```

Output:

```
5
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log k)`
    
    - Inserting into the heap takes `O(log k)` time, and we do it for all `n` elements.
2. **Space Complexity:** `O(k)`
    
    - Extra space is used for the heap of size `k`.

---

## Edge Cases

1. `k = 1` → Return the maximum element.
2. `k = len(nums)` → Return the minimum element.
3. All elements equal → Return that element.

---

## Conclusion

This solution efficiently finds the `k`th largest element using a min-heap, ensuring an optimal time complexity of `O(n log k)`.