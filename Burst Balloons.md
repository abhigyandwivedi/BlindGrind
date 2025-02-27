# 312. Burst Balloons

## Problem Statement

You are given `n` balloons, indexed from `0` to `n - 1`. Each balloon is associated with a number, represented by the array `nums`. You are asked to burst all the balloons.

If you burst balloon `i`, you will get `nums[left] * nums[i] * nums[right]` coins, where `left` and `right` are adjacent balloons of `i`. After bursting `i`, `left` and `right` become adjacent.

Return the **maximum coins** you can collect by bursting the balloons wisely.

### Example 1:

```text
Input: nums = [3,1,5,8]
Output: 167
Explanation:
nums = [3,1,5,8] -> [3,5,8] -> [3,8] -> [8] -> []
Coins = (3*1*5) + (3*5*8) + (1*3*8) + (1*8*1) = 167
```

---

## Solution Approach

We use **dynamic programming** to solve this problem efficiently.

### DP Definition

Let `dp[i][j]` represent the maximum coins we can get by bursting balloons in the range `nums[i]` to `nums[j]`.

### DP Transition

For each balloon `k` in the range `(i, j)`, the profit is calculated as:

```text
dp[i][j] = max(dp[i][k] + nums[i] * nums[k] * nums[j] + dp[k][j])
```

We add virtual balloons `1` at the start and end (`nums = [1] + nums + [1]`).

### Implementation

```python
def maxCoins(nums: list) -> int:
    nums = [1] + nums + [1]
    n = len(nums)
    dp = [[0] * n for _ in range(n)]
    
    for length in range(2, n):
        for left in range(n - length):
            right = left + length
            for k in range(left + 1, right):
                dp[left][right] = max(
                    dp[left][right],
                    dp[left][k] + nums[left] * nums[k] * nums[right] + dp[k][right]
                )
    
    return dp[0][n-1]
```

---

## Complexity Analysis

### Time Complexity

- **O(n³):** We have three nested loops iterating through all possible balloon bursts.

### Space Complexity

- **O(n²):** The DP table stores results for all subproblems.

---

## Example Run

For `nums = [3,1,5,8]`, the maximum coins we can collect is `167`.