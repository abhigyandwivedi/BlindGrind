# 516. Longest Palindromic Subsequence

## Problem Statement

Given a string `s`, return _the length of the longest palindromic subsequence_ in `s`.

A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

### Example 1:

```text
Input: s = "bbbab"
Output: 4
Explanation: The longest palindromic subsequence is "bbbb" and its length is 4.
```

---

## Solution Approach

We use dynamic programming with a 2D table `dp[i][j]`, where `dp[i][j]` represents the length of the longest palindromic subsequence within `s[i:j+1]`.

### DP Transition

1. **Define DP Table:**
    
    - `dp[i][j]` represents the longest palindromic subsequence length within `s[i:j+1]`.
2. **Base Case:**
    
    - If `i == j`, then `dp[i][j] = 1` (a single character is always a palindrome of length 1).
3. **Recurrence Relation:**
    
    - If `s[i] == s[j]`, then these two characters contribute to the palindrome:
        
        ```text
        dp[i][j] = 2 + dp[i+1][j-1]
        ```
        
    - Otherwise, we take the maximum of excluding either character:
        
        ```text
        dp[i][j] = max(dp[i+1][j], dp[i][j-1])
        ```
        

### Implementation

```python
def longestPalindromeSubseq(s: str) -> int:
    n = len(s)
    dp = [[0] * n for _ in range(n)]

    # Base case: Single characters are palindromes of length 1
    for i in range(n):
        dp[i][i] = 1

    # Fill the DP table
    for length in range(2, n + 1):  # Length of the substring
        for i in range(n - length + 1):
            j = i + length - 1
            if s[i] == s[j]:
                dp[i][j] = 2 + dp[i + 1][j - 1]
            else:
                dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])

    return dp[0][n - 1]
```

---

## Complexity Analysis

### Time Complexity

- **O(n²):** We fill an `n x n` DP table, where `n` is the length of `s`.

### Space Complexity

- **O(n²):** The DP table takes `n²` space.
- **Optimized Space:** We can reduce the space complexity to **O(n)** using a rolling array technique.

---

## Example Run

For `s = "bbbab"`, the DP table helps us determine that the longest palindromic subsequence has a length of `4` ("bbbb").