# 96. Unique Binary Search Trees

## Problem Statement

Given an integer `n`, return the number of structurally unique **BSTs** (binary search trees) that store values `1` to `n`.

### Example 1:

```text
Input: n = 3
Output: 5
Explanation:
There are 5 unique BSTs possible for n = 3:
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                \
   2     1         2                3
```

---

## Solution Approach

The problem can be solved using **dynamic programming** with the **Catalan Number** formula.

### DP Formula

Let `dp[i]` represent the number of unique BSTs that can be formed with `i` nodes. The recurrence relation is:

```text
dp[i] = sum(dp[j - 1] * dp[i - j]) for all j in range(1, i + 1)
```

Where:

- `j - 1` nodes form the left subtree.
- `i - j` nodes form the right subtree.

Base Case:

- `dp[0] = 1` (Empty tree is a valid BST)
- `dp[1] = 1` (Only one node forms one BST)

### Implementation

```python
def numTrees(n: int) -> int:
    dp = [0] * (n + 1)
    dp[0], dp[1] = 1, 1
    
    for i in range(2, n + 1):
        for j in range(1, i + 1):
            dp[i] += dp[j - 1] * dp[i - j]
    
    return dp[n]
```

---

## Complexity Analysis

### Time Complexity

- **O(n²):** We iterate through `i` from `2` to `n`, and for each `i`, we iterate through `j` from `1` to `i`.

### Space Complexity

- **O(n):** We use an array `dp` of size `n + 1`.

---

## Example Run

For `n = 3`, the number of unique BSTs is `5`.