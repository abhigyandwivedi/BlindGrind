
# 63: Unique Paths II

## Problem Statement

A robot is located at the top-left corner of a `m x n` grid. The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid.

Now, some cells in the grid are blocked, which means the robot cannot move through them. You need to return the number of unique paths the robot can take to reach the bottom-right corner of the grid.

Note:
- `m` and `n` will be between 1 and 100.
- You can assume that there is at least one path.

### Example 1:
Input: `obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]`  
Output: `2`  
Explanation:  
There are two ways to reach the bottom-right corner:
1. Right → Right → Down → Down
2. Down → Down → Right → Right

### Example 2:
Input: `obstacleGrid = [[0,1,0],[0,1,0],[0,0,0]]`  
Output: `0`  
Explanation:  
There is no way to reach the bottom-right corner because the path is blocked.

### Constraints:
- `m == obstacleGrid.length`
- `n == obstacleGrid[i].length`
- `1 <= m, n <= 100`
- `obstacleGrid[i][j] is 0 or 1`

## Approach

To solve this problem, we can use **Dynamic Programming**. The key idea is to maintain a `dp` table where `dp[i][j]` represents the number of unique paths to reach the cell `(i, j)`.

### Steps:
1. **Base Case**:
   - If the start cell `(0, 0)` is blocked, there are 0 unique paths, so `dp[0][0] = 0`.
   - If the start cell is not blocked, `dp[0][0] = 1`.
   
2. **DP Table Initialization**:
   - For the first row, if there is no obstacle (`obstacleGrid[0][j] == 0`), set `dp[0][j] = dp[0][j-1]` because the only way to move is from left to right.
   - Similarly, for the first column, if there is no obstacle (`obstacleGrid[i][0] == 0`), set `dp[i][0] = dp[i-1][0]` because the only way to move is from top to bottom.
   
3. **Recursive Relation**:
   - For each cell `(i, j)`, if the cell is not blocked (`obstacleGrid[i][j] == 0`), the number of ways to reach `(i, j)` is the sum of the ways to reach the cell from above `(i-1, j)` and from the left `(i, j-1)`:
     ```
     dp[i][j] = dp[i-1][j] + dp[i][j-1]
     ```

4. **Final Answer**:
   - The answer will be stored in `dp[m-1][n-1]`, which represents the number of unique paths to the bottom-right corner of the grid.

### Solution Code:

```python
def uniquePathsWithObstacles(obstacleGrid):
    m, n = len(obstacleGrid), len(obstacleGrid[0])
    
    # Create a DP table
    dp = [[0] * n for _ in range(m)]
    
    # Initialize the start position
    if obstacleGrid[0][0] == 0:
        dp[0][0] = 1

    # Initialize first row
    for j in range(1, n):
        if obstacleGrid[0][j] == 0:
            dp[0][j] = dp[0][j-1]

    # Initialize first column
    for i in range(1, m):
        if obstacleGrid[i][0] == 0:
            dp[i][0] = dp[i-1][0]

    # Fill the DP table
    for i in range(1, m):
        for j in range(1, n):
            if obstacleGrid[i][j] == 0:  # Cell is not blocked
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
    
    return dp[m-1][n-1]
```

## Explanation of the Code:

1. **Initialization**:
   - We first check if the start cell `(0, 0)` is blocked or not.
   - If it's not blocked, we set `dp[0][0] = 1`, indicating one way to start.
   
2. **First Row and First Column**:
   - For the first row, we propagate the number of ways to move from left to right if there are no obstacles.
   - Similarly, for the first column, we propagate the number of ways to move from top to bottom if there are no obstacles.

3. **Filling the DP Table**:
   - We iterate through the remaining cells. For each cell, if it is not blocked, we calculate the number of ways to reach that cell by summing the number of ways to reach the cell from the left and from above.

4. **Final Result**:
   - The final result, which is the number of unique paths to reach the bottom-right corner of the grid, is stored in `dp[m-1][n-1]`.

## Time and Space Complexity:

- **Time Complexity**: O(m * n), where `m` is the number of rows and `n` is the number of columns. We iterate through each cell in the grid exactly once.
- **Space Complexity**: O(m * n), as we use a 2D array `dp` to store the number of unique paths for each cell.

## Example Walkthrough:

For the grid `obstacleGrid = [[0, 0, 0], [0, 1, 0], [0, 0, 0]]`:

1. **Initialization**:
   - The start cell `dp[0][0]` is set to 1 as it is not blocked.
   
2. **Filling First Row**:
   - The first row cells are filled with 1 (indicating one way to reach them from the left) until we reach the second column, where the cell is not blocked.

3. **Filling First Column**:
   - The first column cells are filled similarly until we encounter a blocked cell at `(1, 1)`.

4. **Filling Remaining Cells**:
   - For the remaining cells, the number of unique paths is calculated based on the cells above and to the left.

5. **Final Answer**:
   - The number of unique paths to reach the bottom-right corner is `2`.

## Conclusion

This dynamic programming approach efficiently computes the number of unique paths, taking into account any obstacles in the grid. The solution has a time complexity of O(m * n), making it suitable for the input size constraints.