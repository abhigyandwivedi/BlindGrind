# 712. Minimum ASCII Delete Sum for Two Strings

## Problem Statement

Given two strings `s1` and `s2`, return _the lowest ASCII sum of deleted characters to make the two strings equal_.

### Example 1:

```text
Input: s1 = "sea", s2 = "eat"
Output: 231
Explanation: Deleting "s" from "sea" adds the ASCII value of 's' (115) to the sum. Deleting "t" from "eat" adds 116 to the sum. The total sum is 115 + 116 = 231.
```

### Example 2:

```text
Input: s1 = "delete", s2 = "leet"
Output: 403
Explanation: Deleting "d" and "e" from "delete" adds 100 + 101 = 201. Deleting "e" from "leet" adds 101. The total sum is 201 + 101 = 403.
```

---

## Solution Approach

We can solve this problem using dynamic programming. The idea is to define a 2D DP table where `dp[i][j]` represents the minimum ASCII delete sum required to make the substrings `s1[0..i-1]` and `s2[0..j-1]` equal.

### DP Transition

1. **Base Case:**
    
    - If either string is empty, the cost is the sum of ASCII values of the remaining characters of the other string.
    - `dp[0][j]` = sum of ASCII values of `s2[0..j-1]`
    - `dp[i][0]` = sum of ASCII values of `s1[0..i-1]`
2. **Recurrence Relation:**
    
    - If `s1[i-1] == s2[j-1]`, no deletion is needed for these characters:
        
        ```text
        dp[i][j] = dp[i-1][j-1]
        ```
        
    - Otherwise, we delete one of the characters and take the minimum cost:
        
        ```text
        dp[i][j] = min(dp[i-1][j] + ord(s1[i-1]), dp[i][j-1] + ord(s2[j-1]))
        ```
        

### Implementation

```python
def minimumDeleteSum(s1: str, s2: str) -> int:
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill the base cases
    for i in range(1, m + 1):
        dp[i][0] = dp[i - 1][0] + ord(s1[i - 1])
    for j in range(1, n + 1):
        dp[0][j] = dp[0][j - 1] + ord(s2[j - 1])

    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i - 1] == s2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = min(dp[i - 1][j] + ord(s1[i - 1]), dp[i][j - 1] + ord(s2[j - 1]))

    # Result
    return dp[m][n]
```

---

## Complexity Analysis

### Time Complexity

- **O(m * n):** We fill an `m x n` DP table, where `m` is the length of `s1` and `n` is the length of `s2`.

### Space Complexity

- **O(m * n):** The DP table takes `m * n` space.
- **Optimized Space:** We can reduce space complexity to **O(n)** using a rolling array technique since only the previous row is required to compute the current row.

---

## Example Run

For `s1 = "sea"` and `s2 = "eat"`, the DP table would look like this:

|||e|a|t|
|---|---|---|---|---|
||0|101|198|314|
|s|115|216|313|429|
|e|216|115|212|328|
|a|313|212|115|231|

The final answer is `dp[3][3] = 231`.
