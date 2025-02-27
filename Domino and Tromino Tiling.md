
# 790. Domino and Tromino Tiling

## Problem Statement

You are given an integer `n` representing the height of a 2 × n grid. You need to tile the grid using dominoes (each of size 2 × 1) and trominoes (each of size 2 × 2). Your task is to return the number of ways to tile the grid, modulo 10^9 + 7.

### Problem Breakdown
1. **Domino**: A domino covers exactly 2 cells in the grid.
2. **Tromino**: A tromino covers exactly 3 cells in the grid.

You are tasked with finding the number of ways to tile a grid of height 2 × n using a combination of these two pieces.

## Approach

### Dynamic Programming Approach

This problem can be solved using dynamic programming (DP) by recognizing that the number of ways to tile a grid of size 2 × n depends on smaller subproblems, specifically:
- The number of ways to tile the grid of size 2 × (n-1) and 2 × (n-2), and so on.

Let `dp[i]` represent the number of ways to tile a 2 × i grid.

### Recursive Relation

- If we place a **domino** vertically, we are left with a 2 × (i-1) grid. Thus, `dp[i]` will contribute `dp[i-1]` ways.
- If we place **two dominoes** horizontally, we are left with a 2 × (i-2) grid. Thus, `dp[i]` will contribute `dp[i-2]` ways.
- If we place a **tromino**, we are left with a 2 × (i-3) grid. Thus, `dp[i]` will contribute `dp[i-3]` ways.

Thus, the recursive relation is:
```
dp[i] = dp[i-1] + dp[i-2] + dp[i-3]
```

### Base Cases:
- `dp[0] = 1`: A 2 × 0 grid has exactly one way to be tiled — by using no tiles.
- `dp[1] = 1`: A 2 × 1 grid can only be tiled with one vertical domino.
- `dp[2] = 2`: A 2 × 2 grid can be tiled either with two vertical dominoes or two horizontal dominoes.
- `dp[3] = 4`: A 2 × 3 grid can be tiled with four ways (either using dominoes or one tromino).

### Final Result:
The answer is `dp[n] % (10^9 + 7)`.

## Solution Code

```python
MOD = 10**9 + 7

def numTilings(n: int) -> int:
    # Edge cases for small n
    if n == 0:
        return 1
    if n == 1:
        return 1
    if n == 2:
        return 2
    if n == 3:
        return 4
    
    # Initialize dp array
    dp = [0] * (n + 1)
    
    # Base cases
    dp[0] = 1
    dp[1] = 1
    dp[2] = 2
    dp[3] = 4
    
    # Fill dp array using the recursive relation
    for i in range(4, n + 1):
        dp[i] = (dp[i - 1] + dp[i - 2] + dp[i - 3]) % MOD
    
    return dp[n]
```

## Explanation of the Code:

1. **Initialization**:
   We define `MOD` as 10^9 + 7 to ensure the result is within the required modulo.

2. **Base Cases**:
   We handle small values of `n` directly, returning the precomputed results:
   - For `n = 0`, return `1`.
   - For `n = 1`, return `1`.
   - For `n = 2`, return `2`.
   - For `n = 3`, return `4`.

3. **Dynamic Programming Array (`dp`)**:
   We initialize a DP array of size `n+1`, where each index `i` represents the number of ways to tile a 2 × i grid.

4. **Recursive Relation**:
   Starting from `i = 4`, we fill the `dp` array using the relation `dp[i] = dp[i-1] + dp[i-2] + dp[i-3]`. This ensures we are building on smaller subproblems.

5. **Result**:
   After populating the DP array, we return `dp[n] % MOD`, as we are required to return the result modulo 10^9 + 7.

## Time Complexity:

- **Time Complexity**: O(n), since we are iterating over the array of size `n` once.
- **Space Complexity**: O(n), due to the storage required for the DP array of size `n+1`.

## Example Walkthrough

Consider `n = 4`:

- Base cases: `dp[0] = 1`, `dp[1] = 1`, `dp[2] = 2`, `dp[3] = 4`.
- Compute `dp[4]`:
  ```
  dp[4] = dp[3] + dp[2] + dp[1]
        = 4 + 2 + 1
        = 7
  ```
Thus, the number of ways to tile a 2 × 4 grid is 7.

## Conclusion

This approach efficiently computes the number of ways to tile a 2 × n grid using dynamic programming. The time and space complexity are both O(n), making this solution suitable for large inputs.