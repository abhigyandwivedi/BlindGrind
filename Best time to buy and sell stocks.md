# Solution to "121. Best Time to Buy and Sell Stock"

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

Find the maximum profit you can achieve. You may not engage in multiple transactions (i.e., buy one and sell one share of the stock).

Example:

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6 - 1 = 5.
```

---

## Approach: One Pass (Kadane's Algorithm)

### Explanation

1. **Track Minimum Price:** Traverse the array while tracking the minimum price seen so far.
2. **Calculate Profit:** For each day, calculate the potential profit if sold on that day.
3. **Update Maximum Profit:** Keep track of the maximum profit achieved so far.

---

## Implementation in Python

```python
def maxProfit(prices):
    if not prices:
        return 0

    min_price = prices[0]
    max_profit = 0

    for price in prices[1:]:
        # Update the minimum price
        min_price = min(min_price, price)
        # Calculate potential profit and update max profit
        max_profit = max(max_profit, price - min_price)

    return max_profit

# Example usage
prices = [7, 1, 5, 3, 6, 4]
result = maxProfit(prices)
print(result)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We traverse the array once.
2. **Space Complexity:** `O(1)` - Only constant space is used.

---

## Example Run

Input:

```
prices = [7, 1, 5, 3, 6, 4]
```

Output:

```
5
```

---

## Edge Cases

1. If prices are decreasing, return `0` (no profit possible).
2. If array is empty, return `0`.

---

## Conclusion

This solution efficiently finds the maximum profit by tracking the minimum price and potential profits in a single pass.