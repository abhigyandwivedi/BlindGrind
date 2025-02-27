# Solution to "54. Spiral Matrix"

## Problem Statement

Given an `m x n` matrix, return all elements of the matrix in spiral order.

Example:

```
Input: matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]
Output: [1, 2, 3, 6, 9, 8, 7, 4, 5]
```

---

## Approach: Iterative Layer Traversal

### Explanation

1. **Traverse Boundaries:** Start from the outer boundary and move inward layer by layer.
2. **Four Directions:** Move right, down, left, and up until all elements are traversed.

---

## Implementation in Python

```python
def spiralOrder(matrix: list[list[int]]) -> list[int]:
    result = []
    if not matrix or not matrix[0]:
        return result

    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1

    while top <= bottom and left <= right:
        # Move right
        for i in range(left, right + 1):
            result.append(matrix[top][i])
        top += 1

        # Move down
        for i in range(top, bottom + 1):
            result.append(matrix[i][right])
        right -= 1

        if top <= bottom:
            # Move left
            for i in range(right, left - 1, -1):
                result.append(matrix[bottom][i])
            bottom -= 1

        if left <= right:
            # Move up
            for i in range(bottom, top - 1, -1):
                result.append(matrix[i][left])
            left += 1

    return result
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
print(spiralOrder(matrix))
```

Output:

```
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Every element is visited once.
2. **Space Complexity:** `O(1)`
    
    - Output list excluded; only a few pointers are used.

---

## Edge Cases

1. Empty matrix → Return `[]`.
2. Single row or column → Traverse normally.

---

## Conclusion

This approach efficiently traverses the matrix in spiral order by iterating through layers while maintaining bounds.