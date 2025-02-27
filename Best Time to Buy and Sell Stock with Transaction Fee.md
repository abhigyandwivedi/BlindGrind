# 714. Best Time to Buy and Sell Stock with Transaction Fee

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day and an integer `fee` representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) but you must pay the transaction fee for each sale.

### Example 1:

```text
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: 
Buy on day 1 (price = 1) and sell on day 2 (price = 3), profit = 3-1-2 = 0.
Buy on day 3 (price = 2) and sell on day 4 (price = 8), profit = 8-2-2 = 4.
Buy on day 5 (price = 4) and sell on day 6 (price = 9), profit = 9-4-2 = 3.
Total profit = 0 + 4 + 3 = 8.
```

---

## Solution Approach

We use **dynamic programming** with two states:

1. `hold`: Maximum profit when holding a stock.
2. `cash`: Maximum profit when not holding a stock.

### DP Transition

1. `hold[i] = max(hold[i-1], cash[i-1] - prices[i])` (Buy or keep holding stock)
2. `cash[i] = max(cash[i-1], hold[i-1] + prices[i] - fee)` (Sell and pay the transaction fee)

### Implementation

```python
def maxProfit(prices: list, fee: int) -> int:
    if not prices:
        return 0
    
    hold, cash = -float('inf'), 0
    
    for price in prices:
        prev_cash = cash
        cash = max(cash, hold + price - fee)
        hold = max(hold, prev_cash - price)
    
    return cash
```

---

## Complexity Analysis

### Time Complexity

- **O(n):** We iterate through the prices array once.

### Space Complexity

- **O(1):** We use only a few integer variables.

---

## Example Run

For `prices = [1,3,2,8,4,9]` and `fee = 2`, the maximum profit we can obtain is `8`.