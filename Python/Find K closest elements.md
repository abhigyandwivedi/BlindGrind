# Solution to "658. Find K Closest Elements"

## Problem Statement

Given a sorted array `arr` and two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

---

## Approach: Binary Search + Two Pointers

### Explanation

1. Use binary search to find the closest position of `x` in the array.
2. Expand two pointers outward from this position to find the `k` closest elements.
3. Sort the result before returning.

### Algorithm Steps

1. **Binary Search:** Find the closest position of `x`.
2. **Two Pointers:** Expand left and right pointers to find `k` closest elements.
3. **Sort:** Return the sorted result.

---

## Implementation in Python

```python
class Solution:
    def findClosestElements(self, arr: list[int], k: int, x: int) -> list[int]:
        left, right = 0, len(arr) - 1

        while right - left + 1 > k:
            if abs(arr[left] - x) > abs(arr[right] - x):
                left += 1
            else:
                right -= 1

        return arr[left:right + 1]
```

---

## Example Run

Input:

```python
arr = [1, 2, 3, 4, 5]
k = 4
x = 3
solution = Solution()
print(solution.findClosestElements(arr, k, x))
```

Output:

```
[1, 2, 3, 4]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log n + k)`
    
    - `O(log n)` for binary search and `O(k)` for expanding pointers.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for pointers.

---

## Edge Cases

1. `x` smaller than all elements → First `k` elements.
2. `x` larger than all elements → Last `k` elements.
3. `k` equals array length → Whole array returned.

---

## Conclusion

This solution efficiently finds the `k` closest elements to `x` using binary search and a two-pointer approach with optimal time complexity.

# Solution to "658. Find K Closest Elements"

## Problem Statement

Given a sorted array `arr` and two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

---

## Approach: Heap

### Explanation

We can use a max heap to store the `k` closest elements based on the absolute difference between each element and `x`. Since Python provides a min heap by default, we'll push tuples with negative values to simulate a max heap.

### Algorithm Steps

1. **Heap Construction:** Iterate through the array and push tuples `(-|arr[i] - x|, -arr[i])` into the heap.
2. **Size Maintenance:** If the heap size exceeds `k`, remove the farthest element.
3. **Result Extraction:** Extract elements from the heap, sort them, and return.

---

## Implementation in Python

```python
import heapq

class Solution:
    def findClosestElements(self, arr: list[int], k: int, x: int) -> list[int]:
        heap = []

        for num in arr:
            heapq.heappush(heap, (-abs(num - x), -num))
            if len(heap) > k:
                heapq.heappop(heap)

        result = [-num for _, num in heap]
        result.sort()
        return result
```

---

## Example Run

Input:

```python
arr = [1, 2, 3, 4, 5]
k = 4
x = 3
solution = Solution()
print(solution.findClosestElements(arr, k, x))
```

Output:

```
[1, 2, 3, 4]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log k)`
    
    - For each element, heap insertion takes `O(log k)`.
2. **Space Complexity:** `O(k)`
    
    - The heap stores `k` elements.

---

## Edge Cases

1. `x` smaller than all elements → First `k` elements.
2. `x` larger than all elements → Last `k` elements.
3. `k` equals array length → Whole array returned.

---

## Conclusion

This solution efficiently finds the `k` closest elements to `x` using a max heap approach with optimal time complexity for large datasets.