# 1092. Shortest Common Supersequence

## Problem Statement

Given two strings `str1` and `str2`, return _the shortest string that has both `str1` and `str2` as subsequences_.

### Example 1:

```text
Input: str1 = "abac", str2 = "cab"
Output: "cabac"
Explanation: The shortest common supersequence is "cabac".
```

---

## Solution Approach

We can solve this problem using dynamic programming. The idea is to find the Longest Common Subsequence (LCS) of the two strings and use it to build the shortest common supersequence.

### DP Transition

1. **Define DP Table:**
    
    - `dp[i][j]` represents the length of the LCS of `str1[0..i-1]` and `str2[0..j-1]`.
2. **Base Case:**
    
    - If either string is empty, LCS length is `0`.
3. **Recurrence Relation:**
    
    - If `str1[i-1] == str2[j-1]`:
        
        ```text
        dp[i][j] = 1 + dp[i-1][j-1]
        ```
        
    - Otherwise:
        
        ```text
        dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        ```
        

### Constructing the Supersequence

1. Start from `dp[m][n]` and trace back to build the result.
2. If characters match, include the character once.
3. If they don't match, include the character from the string with the larger value in `dp`.

### Implementation

```python
def shortestCommonSupersequence(str1: str, str2: str) -> str:
    m, n = len(str1), len(str2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if str1[i - 1] == str2[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    # Reconstruct the supersequence
    i, j = m, n
    result = []

    while i > 0 and j > 0:
        if str1[i - 1] == str2[j - 1]:
            result.append(str1[i - 1])
            i -= 1
            j -= 1
        elif dp[i - 1][j] > dp[i][j - 1]:
            result.append(str1[i - 1])
            i -= 1
        else:
            result.append(str2[j - 1])
            j -= 1

    while i > 0:
        result.append(str1[i - 1])
        i -= 1

    while j > 0:
        result.append(str2[j - 1])
        j -= 1

    return ''.join(reversed(result))
```

---

## Complexity Analysis

### Time Complexity

- **O(m * n):** We fill an `m x n` DP table, where `m` is the length of `str1` and `n` is the length of `str2`.

### Space Complexity

- **O(m * n):** The DP table takes `m * n` space.
- **O(m + n):** For the output string construction.

---

## Example Run

For `str1 = "abac"` and `str2 = "cab"`, the DP table would help us build the result `"cabac"`.