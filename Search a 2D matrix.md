# Solution to "74. Search a 2D Matrix"

## Problem Statement

You are given an `m x n` matrix `matrix` with the following properties:

1. Each row is sorted in non-decreasing order.
2. The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if `target` exists in the matrix, and `false` otherwise.

---

## Approach: Binary Search

Since the matrix is sorted both row-wise and column-wise (like a flattened sorted array), we can treat the entire matrix as a single sorted array. We use binary search to find the target efficiently.

### Explanation

1. **Flattening the Matrix Conceptually:**
    
    - Consider the matrix as a single sorted array of size `m * n`.
    - The element at `matrix[i][j]` can be accessed using the index formula:
        
        ```
        row = index // n
        col = index % n
        ```
        
2. **Binary Search:**
    
    - Set `left` to 0 and `right` to `m * n - 1`.
    - While `left <= right`:
        - Find the middle index: `mid = (left + right) // 2`.
        - Find the middle element using `matrix[mid // n][mid % n]`.
        - If the middle element equals the target, return `true`.
        - If the middle element is less than the target, search the right half (`left = mid + 1`).
        - Otherwise, search the left half (`right = mid - 1`).
3. **End Condition:** If the loop ends without finding the target, return `false`.
    

---

## Implementation in Python

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        if not matrix or not matrix[0]:
            return False

        m, n = len(matrix), len(matrix[0])
        left, right = 0, m * n - 1

        while left <= right:
            mid = (left + right) // 2
            mid_element = matrix[mid // n][mid % n]

            if mid_element == target:
                return True
            elif mid_element < target:
                left = mid + 1
            else:
                right = mid - 1

        return False
```

---

## Example Run

Input:

```python
matrix = [
    [1, 3, 5, 7],
    [10, 11, 16, 20],
    [23, 30, 34, 60]
]
target = 3

solution = Solution()
print(solution.searchMatrix(matrix, target))
```

Output:

```
True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log(m * n))`
    
    - We perform binary search on `m * n` elements.
    - Each step reduces the search space by half.
2. **Space Complexity:** `O(1)`
    
    - We use constant space for variables (`left`, `right`, `mid`).

---

## Edge Cases

1. If the matrix is empty (`[]`), return `False`.
2. If `target` is less than the first element or greater than the last element, return `False`.

---

## Conclusion

By leveraging the sorted property of the matrix, we efficiently search for the target using binary search. This solution is optimal in terms of both time and space complexity.