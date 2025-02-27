# 1000. Minimum Cost to Merge Stones

## Problem Statement

You are given an array `stones` where `stones[i]` represents the weight of the `i`-th stone. You can merge `K` consecutive stones into one new stone with a cost equal to the sum of those `K` stones.

Find the minimum cost to merge all stones into one. If it is impossible to do so, return `-1`.

### Example 1:

```text
Input: stones = [3,2,4,1], K = 2
Output: 20
Explanation:
Step 1: Merge [3,2] -> cost = 5
Step 2: Merge [4,1] -> cost = 5
Step 3: Merge [5,5] -> cost = 10
Total Cost = 20
```

---

## Solution Approach

We use **dynamic programming** with prefix sums to optimize merging costs.

### DP Definition

Let `dp[i][j]` represent the minimum cost to merge stones from index `i` to `j`.

### DP Transition

- We iterate over possible partitions and compute costs:

```text
dp[i][j] = min(dp[i][m] + dp[m+1][j]) for all valid m
```

- If `(j - i) % (K - 1) == 0`, we can merge the entire segment:

```text
dp[i][j] += sum(stones[i:j+1])
```

### Implementation

```python
def mergeStones(stones: list, K: int) -> int:
    n = len(stones)
    if (n - 1) % (K - 1) != 0:
        return -1
    
    prefix = [0] * (n + 1)
    for i in range(n):
        prefix[i + 1] = prefix[i] + stones[i]
    
    dp = [[0] * n for _ in range(n)]
    
    for length in range(K, n + 1, K - 1):
        for i in range(n - length + 1):
            j = i + length - 1
            dp[i][j] = min(dp[i][m] + dp[m+1][j] for m in range(i, j, K - 1))
            if (j - i) % (K - 1) == 0:
                dp[i][j] += prefix[j + 1] - prefix[i]
    
    return dp[0][n-1]
```

---

## Complexity Analysis

### Time Complexity

- **O(n³):** We iterate over subarrays and possible merge points.

### Space Complexity

- **O(n²):** We store DP values in a 2D table.

---

## Example Run

For `stones = [3,2,4,1]` and `K = 2`, the minimum cost to merge all stones is `20`.