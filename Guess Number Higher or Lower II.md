# 375. Guess Number Higher or Lower II

## Problem Statement

We are playing a game where I pick a number between `1` and `n`. The goal is to guess the number using the least amount of money. If you guess `x` and the number is different, you pay `x` dollars and continue guessing within the range left.

Find the minimum amount of money required to guarantee a win.

### Example 1:

```text
Input: n = 10
Output: 16
Explanation:
To guarantee a win, the best strategy requires spending at most 16 dollars.
```

---

## Solution Approach

We use **dynamic programming** to find the minimum cost for each possible range.

### DP Definition

Let `dp[i][j]` represent the minimum cost to guarantee a win in the range `[i, j]`.

### DP Transition

For each `k` in `[i, j]`, the cost is:

```text
dp[i][j] = min(k + max(dp[i][k-1], dp[k+1][j])) for all i ≤ k ≤ j
```

where:

- `k` is the current guess.
- We take the worst-case scenario (`max(dp[i][k-1], dp[k+1][j])`) since we must guarantee a win.
- Add `k` since it is the cost of guessing `k` incorrectly.

### Implementation

```python
def getMoneyAmount(n: int) -> int:
    dp = [[0] * (n + 1) for _ in range(n + 1)]
    
    for length in range(2, n + 1):
        for i in range(1, n - length + 2):
            j = i + length - 1
            dp[i][j] = float('inf')
            for k in range(i, j):
                cost = k + max(dp[i][k-1], dp[k+1][j])
                dp[i][j] = min(dp[i][j], cost)
    
    return dp[1][n]
```

---

## Complexity Analysis

### Time Complexity

- **O(n³):** Three nested loops iterate through possible ranges and guesses.

### Space Complexity

- **O(n²):** We use a 2D `dp` table to store results.

---

## Example Run

For `n = 10`, the minimum cost required to guarantee a win is `16`.