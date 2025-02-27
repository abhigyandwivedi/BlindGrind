# 1143. Longest Common Subsequence

## Problem Statement

Given two strings `text1` and `text2`, return _the length of their longest common subsequence_. If there is no common subsequence, return `0`.

### Example 1:

```text
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: The longest common subsequence is "ace" and its length is 3.
```

---

## Solution Approach

We can solve this problem using dynamic programming. The idea is to use a 2D DP table where `dp[i][j]` represents the length of the longest common subsequence of `text1[0..i-1]` and `text2[0..j-1]`.

### DP Transition

1. **Define DP Table:**
    
    - `dp[i][j]` represents the length of the LCS of `text1[0..i-1]` and `text2[0..j-1]`.
2. **Base Case:**
    
    - If either string is empty, the LCS length is `0`.
3. **Recurrence Relation:**
    
    - If `text1[i-1] == text2[j-1]`:
        
        ```text
        dp[i][j] = 1 + dp[i-1][j-1]
        ```
        
    - Otherwise:
        
        ```text
        dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        ```
        

### Implementation

```python
def longestCommonSubsequence(text1: str, text2: str) -> int:
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i - 1] == text2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    return dp[m][n]
```

---

## Complexity Analysis

### Time Complexity

- **O(m * n):** We fill an `m x n` DP table, where `m` is the length of `text1` and `n` is the length of `text2`.

### Space Complexity

- **O(m * n):** The DP table takes `m * n` space.
- **Optimized Space:** We can reduce the space complexity to **O(n)** using a rolling array technique.

---

## Example Run

For `text1 = "abcde"` and `text2 = "ace"`, the DP table would help us find the result `3` for the LCS "ace".