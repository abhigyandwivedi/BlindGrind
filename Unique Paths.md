# Solution to "62. Unique Paths"

## Problem Statement

A robot is located at the top-left corner of an `m x n` grid. The robot can only move either down or right at any point. Find how many unique paths there are to reach the bottom-right corner of the grid.

Example:

```
Input: m = 3, n = 7
Output: 28
```

---

## Approach: Dynamic Programming

### Explanation

1. **DP Table:** Create a 2D table `dp` where `dp[i][j]` represents the number of unique paths to reach cell `(i, j)`.
2. **Base Case:** The first row and first column have only one path (either all rights or all downs).
3. **Transition:** For other cells, `dp[i][j] = dp[i-1][j] + dp[i][j-1]`.
4. **Final Answer:** `dp[m-1][n-1]` gives the total unique paths.

---

## Implementation in Python

```python
def uniquePaths(m, n):
    # Create DP table
    dp = [[1] * n for _ in range(m)]

    # Fill the DP table
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]
```

---

## Example Run

Input:

```python
m = 3
n = 7
print(uniquePaths(m, n))
```

Output:

```
28
```

Explanation:

- The robot can reach the bottom-right corner through 28 unique paths, considering only right and down movements.

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - We fill an `m x n` DP table.
2. **Space Complexity:** `O(m * n)`
    
    - Additional space for the DP table.

---

## Edge Cases

1. If `m` or `n` is `1`, there's only one path.
2. Empty grid (`m = 0` or `n = 0`) returns `0`.

---

## Conclusion

Dynamic programming efficiently computes the number of unique paths for a grid of any size.