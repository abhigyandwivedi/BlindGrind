# Solution to "329. Longest Increasing Path in a Matrix"

## Problem Statement

Given an `m x n` integer matrix, find the length of the longest increasing path in the matrix.

From each cell, you can move in four directions (up, down, left, or right). You may not move diagonally or move outside the boundary. The path can only follow strictly increasing values.

---

## Approach: Depth-First Search (DFS) with Memoization

### Explanation

We can solve this problem using a depth-first search (DFS) with memoization.

### Algorithm Steps

1. **DFS Traversal:**
    
    - Start from each cell and explore all four possible directions.
    - Only move to neighboring cells with a greater value.
2. **Memoization:**
    
    - Use a `cache` matrix where `cache[i][j]` stores the length of the longest increasing path starting from cell `(i, j)`.
3. **Base Case:**
    
    - If the result for a cell is already computed, return the cached value.
4. **Recursion:**
    
    - For each valid move, recursively find the path length and take the maximum.
5. **Result:**
    
    - Iterate through all cells and find the maximum path length.

### Example Walkthrough

For example, given the matrix:

```
matrix = [
    [9, 9, 4],
    [6, 6, 8],
    [2, 1, 1]
]
```

The longest increasing path is `1 → 2 → 6 → 9`, with length `4`.

---

## Implementation in Python

```python
class Solution:
    def longestIncreasingPath(self, matrix: List[List[int]]) -> int:
        if not matrix or not matrix[0]:
            return 0

        m, n = len(matrix), len(matrix[0])
        cache = [[-1] * n for _ in range(m)]

        def dfs(i, j):
            if cache[i][j] != -1:
                return cache[i][j]

            max_len = 1
            for x, y in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
                ni, nj = i + x, j + y
                if 0 <= ni < m and 0 <= nj < n and matrix[ni][nj] > matrix[i][j]:
                    max_len = max(max_len, 1 + dfs(ni, nj))

            cache[i][j] = max_len
            return max_len

        return max(dfs(i, j) for i in range(m) for j in range(n))
```

---

## Example Run

Input:

```python
matrix = [
    [9, 9, 4],
    [6, 6, 8],
    [2, 1, 1]
]
solution = Solution()
print(solution.longestIncreasingPath(matrix))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Each cell is visited once, and results are cached.
2. **Space Complexity:** `O(m * n)`
    
    - Extra space used for memoization.

---

## Edge Cases

1. Empty matrix → Result: `0`
2. Single cell → Result: `1`
3. Matrix with no increasing paths → Result: `1`

---

## Conclusion

This solution efficiently finds the longest increasing path in a matrix using depth-first search with memoization, achieving linear time complexity relative to the number of cells.