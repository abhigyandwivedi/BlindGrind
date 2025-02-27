# 115. Distinct Subsequences

## Problem Statement

Given two strings `s` and `t`, return _the number of distinct subsequences of `s` that equal `t`_.

A subsequence of a string is a new string formed by deleting some (or no) characters without changing the relative order of the remaining characters.

### Example 1:

```text
Input: s = "rabbbit", t = "rabbit"
Output: 3
Explanation:
There are three ways to form "rabbit" from "rabbbit":
1. Remove the first 'b'.
2. Remove the second 'b'.
3. Remove the third 'b'.
```

---

## Solution Approach

We use dynamic programming with a 2D table `dp[i][j]`, where `dp[i][j]` represents the number of distinct subsequences of `s[0..i-1]` that equal `t[0..j-1]`.

### DP Transition

1. **Define DP Table:**
    
    - `dp[i][j]` represents the number of ways to match `s[0..i-1]` with `t[0..j-1]`.
2. **Base Case:**
    
    - If `t` is empty (`j == 0`), there is exactly **one** way to match it (by deleting all characters of `s`).
    - If `s` is empty but `t` is not, no subsequence is possible (`dp[i][j] = 0`).
3. **Recurrence Relation:**
    
    - If `s[i-1] == t[j-1]`, we can either:
        
        1. Include this character in the match (`dp[i-1][j-1]`).
        2. Exclude it and rely on previous subsequences (`dp[i-1][j]`).
        
        ```text
        dp[i][j] = dp[i-1][j] + dp[i-1][j-1]
        ```
        
    - Otherwise, we can only exclude it:
        
        ```text
        dp[i][j] = dp[i-1][j]
        ```
        

### Implementation

```python
def numDistinct(s: str, t: str) -> int:
    m, n = len(s), len(t)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Base case: If t is empty, there's exactly one way (delete all characters)
    for i in range(m + 1):
        dp[i][0] = 1

    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s[i - 1] == t[j - 1]:
                dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1]
            else:
                dp[i][j] = dp[i - 1][j]

    return dp[m][n]
```

---

## Complexity Analysis

### Time Complexity

- **O(m * n):** We fill an `m x n` DP table, where `m` is the length of `s` and `n` is the length of `t`.

### Space Complexity

- **O(m * n):** The DP table takes `m * n` space.
- **Optimized Space:** We can reduce the space complexity to **O(n)** using a rolling array technique.

---

## Example Run

For `s = "rabbbit"` and `t = "rabbit"`, the DP table helps us determine that there are `3` distinct subsequences.