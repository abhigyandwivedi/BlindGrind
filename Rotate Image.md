# Solution to "48. Rotate Image"

## Problem Statement

Given an `n x n` 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

- You must rotate the image in-place, meaning you cannot allocate another 2D matrix to perform the rotation.

---

## Approach: Transpose and Reverse

### Explanation

We can achieve the rotation in two steps:

1. **Transpose the Matrix:**
    
    - Convert rows into columns by swapping `matrix[i][j]` with `matrix[j][i]`.
2. **Reverse Each Row:**
    
    - Reverse each row to complete the clockwise rotation.

### Example Walkthrough

For example, given the matrix:

```
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]
```

**Step 1: Transpose the matrix:**

```
[
 [1, 4, 7],
 [2, 5, 8],
 [3, 6, 9]
]
```

**Step 2: Reverse each row:**

```
[
 [7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]
]
```

---

## Implementation in Python

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)
        # Step 1: Transpose the matrix
        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # Step 2: Reverse each row
        for row in matrix:
            row.reverse()
```

---

## Example Run

Input:

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

solution = Solution()
solution.rotate(matrix)
print(matrix)
```

Output:

```
[
 [7, 4, 1],
 [8, 5, 2],
 [9, 6, 3]
]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N^2)`
    
    - Transposing the matrix takes `O(N^2)` time.
    - Reversing each row takes `O(N)` per row, resulting in `O(N^2)` overall.
2. **Space Complexity:** `O(1)`
    
    - In-place rotation requires constant extra space.

---

## Edge Cases

1. If the matrix is empty, no rotation is needed.
2. For a `1 x 1` matrix, the output is the same as the input.
3. Works for both even and odd-sized matrices.

---

## Conclusion

This efficient in-place solution rotates the matrix by 90 degrees clockwise using transposition followed by row reversal.