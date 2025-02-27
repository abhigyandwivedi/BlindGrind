# 72. Edit Distance

## Problem Statement

Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_. The allowed operations are:

1. Insert a character
2. Delete a character
3. Replace a character

### Example 1:

```text
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
1. Replace 'h' with 'r' -> "rorse"
2. Remove 'r' -> "rose"
3. Remove 'e' -> "ros"
```

---

## Solution Approach

We solve this problem using dynamic programming. The idea is to define a 2D DP table where `dp[i][j]` represents the minimum number of operations required to convert `word1[0..i-1]` to `word2[0..j-1]`.

### DP Transition

1. **Define DP Table:**
    
    - `dp[i][j]` represents the edit distance between `word1[0..i-1]` and `word2[0..j-1]`.
2. **Base Case:**
    
    - If `word1` is empty, the only option is to insert all characters from `word2` (`dp[0][j] = j`).
    - If `word2` is empty, the only option is to delete all characters from `word1` (`dp[i][0] = i`).
3. **Recurrence Relation:**
    
    - If `word1[i-1] == word2[j-1]`, no change is needed:
        
        ```text
        dp[i][j] = dp[i-1][j-1]
        ```
        
    - Otherwise, consider the three operations:
        
        ```text
        dp[i][j] = 1 + min(dp[i-1][j],    # Delete
                            dp[i][j-1],    # Insert
                            dp[i-1][j-1])  # Replace
        ```
        

### Implementation

```python
def minDistance(word1: str, word2: str) -> int:
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill base cases
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j

    # Fill the DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i - 1] == word2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = 1 + min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1])

    return dp[m][n]
```

---

## Complexity Analysis

### Time Complexity

- **O(m * n):** We fill an `m x n` DP table, where `m` is the length of `word1` and `n` is the length of `word2`.

### Space Complexity

- **O(m * n):** The DP table takes `m * n` space.
- **Optimized Space:** We can reduce the space complexity to **O(n)** using a rolling array technique.

---

## Example Run

For `word1 = "horse"` and `word2 = "ros"`, the DP table helps us determine the minimum edit distance of `3`.