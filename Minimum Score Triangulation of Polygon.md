# 1039. Minimum Score Triangulation of Polygon

## Problem Statement

You are given an array `values` where `values[i]` represents the value of the `i`-th vertex of a polygon. The goal is to triangulate the polygon by forming non-overlapping triangles and minimizing the total score. The score of a triangle formed by vertices `(i, j, k)` is `values[i] * values[j] * values[k]`.

Find the minimum possible total score of triangulating the polygon.

### Example 1:

```text
Input: values = [1,3,1,4,1,5]
Output: 13
Explanation:
The optimal triangulation is [(1,3,4), (3,4,1), (4,1,5)], which gives the minimum score of 13.
```

---

## Solution Approach

We use **dynamic programming** to find the optimal way to triangulate the polygon.

### DP Definition

Let `dp[i][j]` represent the minimum triangulation score for the polygon between indices `i` and `j`.

### DP Transition

- We iterate over possible partitions `k` where `i < k < j`, computing:

```text
dp[i][j] = min(dp[i][k] + dp[k][j] + values[i] * values[k] * values[j])
```

### Implementation

```python
def minScoreTriangulation(values: list) -> int:
    n = len(values)
    dp = [[float('inf')] * n for _ in range(n)]
    
    for i in range(n - 1):
        dp[i][i+1] = 0  # No cost for a line segment
    
    for length in range(2, n):  # Length of the segment
        for i in range(n - length):
            j = i + length
            for k in range(i + 1, j):
                dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j] + values[i] * values[k] * values[j])
    
    return dp[0][n-1]
```

---

## Complexity Analysis

### Time Complexity

- **O(n³):** We iterate over all possible subarrays and partitions.

### Space Complexity

- **O(n²):** We store DP values in a 2D table.

---

## Example Run

For `values = [1,3,1,4,1,5]`, the minimum score triangulation is `13`.