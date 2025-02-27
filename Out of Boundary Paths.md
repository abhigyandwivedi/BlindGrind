
# 576: Out of Boundary Paths

## Problem Statement

There is an `m x n` grid. On the grid, we start at position `(startRow, startColumn)` and walk according to the following rules:

- We can walk on four directions: left, right, up, down.
- Every time we step outside the grid, we leave the grid and the walk ends.
- Return the number of paths that start at `(startRow, startColumn)` and end outside the grid after walking exactly `steps` steps.

### Example 1:
Input: `m = 3, n = 3, maxMove = 3, startRow = 0, startColumn = 0`  
Output: `12`

### Example 2:
Input: `m = 3, n = 3, maxMove = 3, startRow = 1, startColumn = 1`  
Output: `6`

### Example 3:
Input: `m = 3, n = 3, maxMove = 3, startRow = 0, startColumn = 2`  
Output: `2`

### Constraints:
- 1 <= `m, n <= 50`
- 0 <= `maxMove <= 50`
- 0 <= `startRow < m`
- 0 <= `startColumn < n`

## Approach

This problem can be solved using **Dynamic Programming (DP)**. We need to track the number of ways to reach each position in the grid with a given number of steps. If we step outside the boundary of the grid, the walk ends, and we count that as a valid path.

### Key Ideas:

1. **Grid Representation**:
   - We have a grid of size `m x n`. We will maintain a DP table where `dp[k][x][y]` represents the number of ways to reach position `(x, y)` with exactly `k` steps.

2. **Base Case**:
   - If we step out of the boundary of the grid, we count that as a valid path. Therefore, if `x < 0`, `x >= m`, `y < 0`, or `y >= n`, the current state should be treated as a valid exit.

3. **Transition**:
   - From each cell `(x, y)` with `k` steps remaining, the knight can move to any of the four directions (up, down, left, right). The number of paths to reach `(x, y)` with `k` steps will be the sum of paths to its neighboring cells at `k-1` steps.

4. **Modulo Operation**:
   - Since the result can be large, return the final answer modulo `10^9 + 7`.

5. **Space Optimization**:
   - We can optimize the space by only keeping track of the current and previous step, reducing the space complexity to O(m * n).

### Solution Code

```python
MOD = 10**9 + 7

def findPaths(m, n, maxMove, startRow, startColumn):
    # DP table, we use two 2D arrays to save space (current and previous)
    dp_prev = [[0] * n for _ in range(m)]
    dp_curr = [[0] * n for _ in range(m)]
    
    # Base case: the starting point (startRow, startColumn)
    dp_prev[startRow][startColumn] = 1
    
    # Iterate through the number of steps
    for move in range(1, maxMove + 1):
        for i in range(m):
            for j in range(n):
                # If we're not out of bounds, calculate the number of ways to move to (i, j)
                if dp_prev[i][j] > 0:
                    if i > 0: dp_curr[i-1][j] = (dp_curr[i-1][j] + dp_prev[i][j]) % MOD
                    if i < m-1: dp_curr[i+1][j] = (dp_curr[i+1][j] + dp_prev[i][j]) % MOD
                    if j > 0: dp_curr[i][j-1] = (dp_curr[i][j-1] + dp_prev[i][j]) % MOD
                    if j < n-1: dp_curr[i][j+1] = (dp_curr[i][j+1] + dp_prev[i][j]) % MOD
        
        # Reset dp_prev to dp_curr and clear dp_curr for the next iteration
        dp_prev, dp_curr = dp_curr, [[0] * n for _ in range(m)]
    
    # Final answer: sum all the boundary cells in dp_prev
    result = 0
    for i in range(m):
        result = (result + dp_prev[i][0]) % MOD
        result = (result + dp_prev[i][n-1]) % MOD
    for j in range(n):
        result = (result + dp_prev[0][j]) % MOD
        result = (result + dp_prev[m-1][j]) % MOD
    
    return result
```

## Explanation of the Code:

1. **Initialization**: 
   - We initialize two 2D arrays `dp_prev` and `dp_curr`, which track the number of paths to each cell at the current and previous steps respectively.
   - We set `dp_prev[startRow][startColumn] = 1` to indicate that there is one way to start at `(startRow, startColumn)`.

2. **Dynamic Programming Loop**:
   - For each number of moves from 1 to `maxMove`, we update the `dp_curr` table based on `dp_prev` by considering all four possible moves (up, down, left, right).
   - After each iteration, `dp_prev` is updated to be the `dp_curr` table, and `dp_curr` is reset for the next iteration.

3. **Boundary Check**:
   - After completing all the steps, we sum up the values in the boundary cells of `dp_prev` (i.e., the first and last row and column) because any path that reaches the boundary of the grid is considered a valid path that goes out of the boundary.

4. **Modulo Operation**:
   - The result is taken modulo `10^9 + 7` to handle large numbers as required by the problem constraints.

## Time and Space Complexity:

- **Time Complexity**: O(m * n * maxMove). 
  - We iterate over each possible number of steps (up to `maxMove`), and for each step, we iterate over every cell in the `m x n` grid.

- **Space Complexity**: O(m * n). 
  - We use two 2D arrays (`dp_prev` and `dp_curr`) to store the number of ways to reach each cell in the grid at the current and previous steps.

## Example Walkthrough:

For `m = 3, n = 3, maxMove = 3, startRow = 0, startColumn = 0`:

1. **Initialization**:
   - `dp_prev[0][0] = 1` because the knight starts at `(0, 0)`.

2. **After 1 Move**:
   - From `(0, 0)`, the knight can move to `(1, 0)` and `(0, 1)`.

3. **After 2 Moves**:
   - The knight can move from `(1, 0)` and `(0, 1)` to new positions, and we update `dp_curr`.

4. **After 3 Moves**:
   - The knight can continue moving and update the probabilities of reaching different positions.

5. **Final Answer**:
   - After 3 moves, sum the probabilities of the boundary cells `(0, 0)`, `(0, 2)`, `(2, 0)`, and `(2, 2)` to get the total number of paths that lead out of the boundary.

Thus, the final output is `12`.

## Conclusion

This dynamic programming approach efficiently computes the number of paths that lead out of the boundary after exactly `maxMove` moves. The time and space complexities are manageable, given the problem's constraints.