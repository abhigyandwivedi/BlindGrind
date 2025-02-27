
# Best Time to Buy and Sell Stock II

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`-th day.

You can buy and sell the stock multiple times, but you need to follow the following rules:
- You must sell the stock before you buy again.
- You cannot engage in multiple transactions at the same time (i.e., you must sell the stock before buying again).

Your goal is to maximize the profit you can make.

## Solution Explanation

### Approach

In this problem, you are allowed to make multiple transactions, but there are no restrictions on how many times you can buy and sell the stock. The strategy to maximize profit is to sell the stock whenever there is a price increase. So, if the price of the stock on day `i+1` is greater than the price on day `i`, we buy the stock on day `i` and sell it on day `i+1`. The profit in that transaction would be the difference between the prices of the two days.

### Steps to Solve the Problem
1. Initialize a variable `profit` to store the total profit.
2. Traverse through the `prices` array.
3. For each consecutive pair of days, if the price on the next day is higher than the price on the current day, add the difference (i.e., `prices[i+1] - prices[i]`) to the `profit`.
4. Return the total profit after completing the loop.

### Code Implementation

```python
def maxProfit(prices):
    profit = 0
    for i in range(1, len(prices)):
        if prices[i] > prices[i-1]:
            profit += prices[i] - prices[i-1]
    return profit
```

### Detailed Explanation
- We start by initializing `profit` as 0, since we have not made any transactions yet.
- We then iterate through the `prices` array starting from index 1.
- If the price on the next day (`prices[i]`) is greater than the price on the current day (`prices[i-1]`), this means that we can make a profit by selling on the next day, so we add the difference (`prices[i] - prices[i-1]`) to the `profit`.
- This continues until we have traversed through all the days.

### Example

Let’s walk through an example:

**Input:** `prices = [7, 1, 5, 3, 6, 4]`

- Day 1 to Day 2: Price drops (1 < 7), do nothing.
- Day 2 to Day 3: Price increases (5 > 1), profit = 5 - 1 = 4.
- Day 3 to Day 4: Price drops (3 < 5), do nothing.
- Day 4 to Day 5: Price increases (6 > 3), profit += 6 - 3 = 7.
- Day 5 to Day 6: Price drops (4 < 6), do nothing.

**Total profit:** 4 + 7 = 11

**Output:** `11`

### Time Complexity

- The time complexity of this solution is **O(n)**, where `n` is the number of days (the length of the `prices` array). We iterate through the list once to calculate the total profit.

### Space Complexity

- The space complexity is **O(1)** because we only use a constant amount of extra space (the `profit` variable).

## Conclusion

This approach efficiently computes the maximum profit in linear time by taking advantage of the fact that we can profit from every increase in the stock price. By adding the profit on each increase, we can ensure that we make the most profit possible in multiple transactions.