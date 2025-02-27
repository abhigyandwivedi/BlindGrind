# Solution to "4. Median of Two Sorted Arrays"

## Problem Statement

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

---

## Approach: Binary Search

### Explanation

We use binary search on the smaller array to partition both arrays such that the left half contains smaller elements and the right half contains larger elements.

### Algorithm Steps

1. **Binary Search:** Perform binary search on the smaller array.
2. **Partition:** Find partitions such that the left of both arrays are less than the right.
3. **Median Calculation:**
    - If combined length is even, take the average of the max left and min right.
    - If odd, take the max left.

---

## Implementation in Python

```python
class Solution:
    def findMedianSortedArrays(self, nums1: list[int], nums2: list[int]) -> float:
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1

        x, y = len(nums1), len(nums2)
        low, high = 0, x

        while low <= high:
            partitionX = (low + high) // 2
            partitionY = (x + y + 1) // 2 - partitionX

            maxX = float('-inf') if partitionX == 0 else nums1[partitionX - 1]
            minX = float('inf') if partitionX == x else nums1[partitionX]

            maxY = float('-inf') if partitionY == 0 else nums2[partitionY - 1]
            minY = float('inf') if partitionY == y else nums2[partitionY]

            if maxX <= minY and maxY <= minX:
                if (x + y) % 2 == 0:
                    return (max(maxX, maxY) + min(minX, minY)) / 2
                else:
                    return max(maxX, maxY)
            elif maxX > minY:
                high = partitionX - 1
            else:
                low = partitionX + 1
```

---

## Example Run

Input:

```python
nums1 = [1, 3]
nums2 = [2]
solution = Solution()
print(solution.findMedianSortedArrays(nums1, nums2))
```

Output:

```
2.0
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log(min(m, n)))`
    
    - Binary search on the smaller array.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for variables.

---

## Edge Cases

1. One array empty → Median from the non-empty array.
2. Both arrays empty → Undefined behavior.
3. Arrays of different sizes → Handled by partitioning.

---

## Conclusion

This solution efficiently finds the median of two sorted arrays using binary search with optimal time complexity.