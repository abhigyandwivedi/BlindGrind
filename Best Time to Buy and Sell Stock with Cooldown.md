# 309. Best Time to Buy and Sell Stock with Cooldown

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

Find the maximum profit you can achieve. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times) with the following restriction:

- After you sell your stock, you cannot buy stock on the next day (i.e., cooldown for one day).

### Example 1:

```text
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: 
Buy on day 1 (price = 1) and sell on day 2 (price = 2), profit = 1.
Cooldown on day 3.
Buy on day 4 (price = 0) and sell on day 5 (price = 2), profit = 2.
Total profit = 1 + 2 = 3.
```

---

## Solution Approach

We use **dynamic programming** with three states:

1. `hold`: Maximum profit when holding a stock.
2. `sold`: Maximum profit when selling a stock.
3. `rest`: Maximum profit when in cooldown.

### DP Transition

1. `hold[i] = max(hold[i-1], rest[i-1] - prices[i])` (Buy or keep holding stock)
2. `sold[i] = hold[i-1] + prices[i]` (Sell stock)
3. `rest[i] = max(rest[i-1], sold[i-1])` (Cooldown or remain in cooldown state)

### Implementation

```python
def maxProfit(prices: list) -> int:
    if not prices:
        return 0
    
    n = len(prices)
    hold, sold, rest = -float('inf'), 0, 0
    
    for price in prices:
        prev_sold = sold
        sold = hold + price
        hold = max(hold, rest - price)
        rest = max(rest, prev_sold)
    
    return max(sold, rest)
```

---

## Complexity Analysis

### Time Complexity

- **O(n):** We iterate through the prices array once.

### Space Complexity

- **O(1):** We use only a few integer variables.

---

## Example Run

For `prices = [1,2,3,0,2]`, the maximum profit we can obtain with a **cooldown** constraint is `3`.