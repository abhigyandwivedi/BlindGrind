# Solution to "221. Maximal Square"

## Problem Statement

Given an `m x n` binary matrix filled with `0`s and `1`s, find the largest square containing only `1`s and return its area.

---

## Approach: Dynamic Programming

### Explanation

We can use a **Dynamic Programming (DP)** approach to solve this problem efficiently.

1. **DP Table:**
    
    - Create a 2D DP array `dp` where `dp[i][j]` represents the side length of the largest square whose bottom-right corner is `matrix[i][j]`.
2. **Recurrence Relation:**
    
    - If `matrix[i][j]` is `1`, calculate:
        
        ```
        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
        ```
        
    - If `matrix[i][j]` is `0`, set `dp[i][j] = 0`.
3. **Track Maximum Side:**
    
    - Keep track of the maximum side length `max_side` while filling the DP table.
4. **Result:**
    
    - The area of the maximal square is `max_side * max_side`.

### Example Walkthrough

For example, given the matrix:

```
[
 ["1", "0", "1", "0", "0"],
 ["1", "0", "1", "1", "1"],
 ["1", "1", "1", "1", "1"],
 ["1", "0", "0", "1", "0"]
]
```

**DP Table after processing:**

```
[
 [1, 0, 1, 0, 0],
 [1, 0, 1, 1, 1],
 [1, 1, 1, 2, 2],
 [1, 0, 0, 1, 0]
]
```

Maximum side length = `2`, thus area = `2 * 2 = 4`.

---

## Implementation in Python

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix or not matrix[0]:
            return 0
        
        m, n = len(matrix), len(matrix[0])
        dp = [[0] * n for _ in range(m)]
        max_side = 0
        
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == '1':
                    if i == 0 or j == 0:
                        dp[i][j] = 1
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
                    max_side = max(max_side, dp[i][j])
        
        return max_side * max_side
```

---

## Example Run

Input:

```python
matrix = [
    ["1", "0", "1", "0", "0"],
    ["1", "0", "1", "1", "1"],
    ["1", "1", "1", "1", "1"],
    ["1", "0", "0", "1", "0"]
]

solution = Solution()
print(solution.maximalSquare(matrix))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - We traverse the entire matrix once, where `m` is the number of rows and `n` is the number of columns.
2. **Space Complexity:** `O(m * n)`
    
    - We use a DP table of the same size as the input matrix.

_Optimized Approach:_ Using a 1D array reduces space complexity to `O(n)`.

---

## Edge Cases

1. If the matrix is empty, return `0`.
2. If all cells are `0`, return `0`.
3. If all cells are `1`, return the area of the entire matrix.

---

## Conclusion

This dynamic programming solution efficiently finds the largest square of `1`s in a binary matrix and returns its area.