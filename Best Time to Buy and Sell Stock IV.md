# 188. Best Time to Buy and Sell Stock IV

## Problem Statement

You are given an integer `k` and an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

Find the maximum profit you can achieve. You may complete at most **k** transactions.

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before buying again).

### Example 1:

```text
Input: k = 2, prices = [3,2,6,5,0,3]
Output: 7
Explanation: 
Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Total profit = 4 + 3 = 7.
```

---

## Solution Approach

We use a **dynamic programming** approach where we define `dp[i][j]` as the maximum profit on day `j` with at most `i` transactions.

### DP Transition

1. **Define DP Table:**
    - `dp[i][j]` represents the maximum profit achievable on day `j` with at most `i` transactions.
2. **Base Case:**
    - If `k == 0` or `prices` is empty, `dp[i][j] = 0`.
3. **Recurrence Relation:**
    - For each transaction `i`, track the maximum of `(dp[i-1][m] - prices[m])` for all `m < j`.
    - This leads to:
        
        ```text
        dp[i][j] = max(dp[i][j-1], prices[j] + max_profit_before)
        ```
        
    - Where `max_profit_before = max(dp[i-1][m] - prices[m])` for all `m < j`.

### Implementation

```python
def maxProfit(k: int, prices: list) -> int:
    if not prices or k == 0:
        return 0
    
    n = len(prices)
    if k >= n // 2:
        return sum(max(prices[i+1] - prices[i], 0) for i in range(n-1))
    
    dp = [[0] * n for _ in range(k + 1)]
    
    for i in range(1, k + 1):
        max_profit_before = float('-inf')
        for j in range(1, n):
            max_profit_before = max(max_profit_before, dp[i-1][j-1] - prices[j-1])
            dp[i][j] = max(dp[i][j-1], prices[j] + max_profit_before)
    
    return dp[k][n-1]
```

---

## Complexity Analysis

### Time Complexity

- **O(k * n):** We iterate through `k` transactions and `n` days.

### Space Complexity

- **O(k * n):** The DP table takes `k * n` space.
- **Optimized Space:** We can reduce space complexity to **O(n)** using a rolling array.

---

## Example Run

For `k = 2` and `prices = [3,2,6,5,0,3]`, the maximum profit we can obtain with at most **2 transactions** is `7`.