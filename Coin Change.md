# Solution to "322. Coin Change"

## Problem Statement

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the fewest number of coins needed to make up that amount. If that amount cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

Example:

```
Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

Input: coins = [2], amount = 3
Output: -1
```

---

## Approach: Dynamic Programming

### Explanation

1. Create a `dp` array where `dp[i]` represents the minimum number of coins needed to make amount `i`.
2. Initialize `dp[0] = 0` and set all other `dp[i]` values to infinity (`float('inf')`).
3. For each coin, update `dp[j]` for all amounts `j` from `coin` to `amount` using the formula:

```
dp[j] = min(dp[j], dp[j - coin] + 1)
```

1. If `dp[amount]` remains infinity, return `-1`; otherwise, return `dp[amount]`.

---

## Implementation in Python

```python
def coinChange(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0

    for coin in coins:
        for j in range(coin, amount + 1):
            dp[j] = min(dp[j], dp[j - coin] + 1)

    return dp[amount] if dp[amount] != float('inf') else -1

# Example usage
coins = [1, 2, 5]
amount = 11
print(coinChange(coins, amount))  # Output: 3
```

---

## Example Run

Input:

```python
coins = [1, 2, 5]
amount = 11
print(coinChange(coins, amount))  # Output: 3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n * m)` where `n` is the `amount` and `m` is the number of coin denominations. We iterate through each coin and each possible amount.
2. **Space Complexity:** `O(n)` for the `dp` array storing results up to `amount`.

---

## Edge Cases

1. No solution: `coins = [2]`, `amount = 3` → Output: `-1`
2. Zero amount: `coins = [1, 2, 5]`, `amount = 0` → Output: `0`
3. Single coin equals amount: `coins = [10]`, `amount = 10` → Output: `1`

---

## Conclusion

This solution efficiently computes the minimum number of coins needed for a given amount using dynamic programming, ensuring an optimal solution with reasonable time complexity.