# 546. Remove Boxes

## Problem Statement

You are given several boxes with different colors represented by an array `boxes`, where `boxes[i]` is the color of the `i`-th box. You can remove boxes according to the following rule:

- If you remove `k` consecutive boxes of the same color, you earn `k * k` points.
- The remaining boxes will shift to fill the gaps.
- Find the maximum points you can earn by removing the boxes optimally.

### Example 1:

```text
Input: boxes = [1,3,2,2,2,3,4,3,1]
Output: 23
Explanation:
Remove [2,2,2] → 3*3 = 9 points
Remove [3,3,3] → 3*3 = 9 points
Remove [1,4,1] → 1*1 + 1*1 + 1*1 = 3 points
Total = 23
```

---

## Solution Approach

We use **dynamic programming** with a 3D `dp` table to optimize the removal of boxes.

### DP Definition

Let `dp[i][j][k]` represent the maximum points we can get by removing boxes from index `i` to `j`, where there are `k` extra boxes of the same color as `boxes[i]` to the left.

### DP Transition

1. Remove the `i`-th box and its `k` extra adjacent boxes:

```text
dp[i][j][k] = (k+1) * (k+1) + dp[i+1][j][0]
```

1. Try merging `boxes[i]` with another occurrence in `[i+1, j]`:

```text
dp[i][j][k] = max(dp[i][j][k], dp[i+1][m-1][0] + dp[m][j][k+1])
```

for `m` where `boxes[m] == boxes[i]`.

### Implementation

```python
def removeBoxes(boxes: list) -> int:
    from functools import lru_cache
    
    @lru_cache(None)
    def dp(i, j, k):
        if i > j:
            return 0
        while i < j and boxes[i] == boxes[i+1]:
            i += 1
            k += 1
        
        result = (k+1) * (k+1) + dp(i+1, j, 0)
        
        for m in range(i+1, j+1):
            if boxes[m] == boxes[i]:
                result = max(result, dp(i+1, m-1, 0) + dp(m, j, k+1))
        
        return result
    
    return dp(0, len(boxes)-1, 0)
```

---

## Complexity Analysis

### Time Complexity

- **O(n³):** We have three nested loops for different partitions of `boxes`.

### Space Complexity

- **O(n³):** The memoization table stores results for all subproblems.

---

## Example Run

For `boxes = [1,3,2,2,2,3,4,3,1]`, the maximum points we can earn is `23`.