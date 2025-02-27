# 123. Best Time to Buy and Sell Stock III

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

Find the maximum profit you can achieve. You may complete at most **two** transactions.

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before buying again).

### Example 1:

```text
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: 
Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
Total profit = 3 + 3 = 6.
```

---

## Solution Approach

We use a dynamic programming approach where we track **four states**:

1. `buy1` - The maximum profit after buying the first stock.
2. `sell1` - The maximum profit after selling the first stock.
3. `buy2` - The maximum profit after buying the second stock.
4. `sell2` - The maximum profit after selling the second stock.

### State Transitions:

- `buy1 = max(buy1, -prices[i])` → Buy at a lower price.
- `sell1 = max(sell1, buy1 + prices[i])` → Sell for a higher profit.
- `buy2 = max(buy2, sell1 - prices[i])` → Buy again after the first sell.
- `sell2 = max(sell2, buy2 + prices[i])` → Sell again for maximum profit.

### Implementation

```python
def maxProfit(prices):
    buy1, sell1 = float('-inf'), 0
    buy2, sell2 = float('-inf'), 0
    
    for price in prices:
        buy1 = max(buy1, -price)        # First buy
        sell1 = max(sell1, buy1 + price) # First sell
        buy2 = max(buy2, sell1 - price)  # Second buy
        sell2 = max(sell2, buy2 + price) # Second sell
    
    return sell2
```

---

## Complexity Analysis

### Time Complexity

- **O(n):** We iterate through the prices array once.

### Space Complexity

- **O(1):** We use only a few integer variables.

---

## Example Run

For `prices = [3,3,5,0,0,3,1,4]`, the maximum profit we can obtain with at most **two transactions** is `6`.