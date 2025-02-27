
# 688: Knight Probability in Chessboard

## Problem Statement

On an `n x n` chessboard, a knight starts at the cell `(row, column)` and moves according to the rules of chess. The knight can move to 8 different positions, but some of them may fall off the chessboard. 

Given the integer `n` and the knight’s starting position `(row, column)`, return the probability that the knight will still be on the board after `k` moves.

### Example 1:
Input: `n = 3, k = 2, row = 0, column = 0`  
Output: `0.0625`

### Example 2:
Input: `n = 1, k = 0, row = 0, column = 0`  
Output: `1`

### Constraints:
- 1 <= `n <= 25`
- 0 <= `k <= 100`
- 0 <= `row, column < n`

## Approach

The problem can be solved using **Dynamic Programming** (DP). Since the knight’s movement is probabilistic and involves multiple stages (each stage being a move), we can use DP to track the probability of the knight being on the board after each move.

### Key Ideas:

1. **Knight’s Moves**: A knight can move in 8 directions, defined by the following relative moves:
   - `(2, 1)`, `(2, -1)`, `(-2, 1)`, `(-2, -1)`
   - `(1, 2)`, `(1, -2)`, `(-1, 2)`, `(-1, -2)`

2. **Recursive Relation**: At any given point, the knight can move from a position `(x, y)` to a new position `(x', y')`. The knight has equal probability of moving to any of the 8 possible positions (if they are within the bounds of the board).

3. **Dynamic Programming Array**: 
   - Use a 3D DP array `dp[k][x][y]` where `dp[k][x][y]` represents the probability of being at position `(x, y)` after `k` moves.
   - Initialize the probability of the knight starting at `(row, column)` with `dp[0][row][column] = 1`.
   - For each subsequent move `k`, calculate the probability of reaching each position `(x, y)` based on the previous step.

4. **Base Case**: 
   - The knight starts at position `(row, column)` with probability `1` at `k = 0`.
   
5. **Transition**:
   - For each step from `k = 1` to `k = k`, for each possible position `(x, y)`, the probability is the sum of the probabilities of the 8 possible preceding positions (if they are within bounds).

6. **Final Answer**: After completing all the moves, sum the probabilities of all positions `(x, y)` that are within the bounds of the chessboard.

### Solution Code

```python
def knightProbability(n, k, row, column):
    # Directions a knight can move
    directions = [(2, 1), (2, -1), (-2, 1), (-2, -1), 
                  (1, 2), (1, -2), (-1, 2), (-1, -2)]
    
    # DP table to store probabilities
    dp = [[[0] * n for _ in range(n)] for _ in range(k + 1)]
    dp[0][row][column] = 1  # Starting point has probability 1
    
    # Iterate for each move
    for step in range(1, k + 1):
        for x in range(n):
            for y in range(n):
                # Calculate the probability for each move to position (x, y)
                for dx, dy in directions:
                    prev_x, prev_y = x - dx, y - dy
                    if 0 <= prev_x < n and 0 <= prev_y < n:
                        dp[step][x][y] += dp[step - 1][prev_x][prev_y] / 8
    
    # Sum all probabilities for the last move
    result = 0
    for x in range(n):
        for y in range(n):
            result += dp[k][x][y]
    
    return result
```

## Explanation of the Code:

1. **Initialization**: 
   - We initialize a 3D list `dp` with dimensions `(k + 1) x n x n`, where `dp[i][x][y]` stores the probability of the knight being at position `(x, y)` after `i` moves.
   - We start with `dp[0][row][column] = 1`, indicating that the knight starts at the given position with a probability of `1`.

2. **Recursive DP Update**: 
   - We iterate over each move `step` from `1` to `k`. For each position `(x, y)` on the board, we check all 8 possible moves a knight could have made to reach that position.
   - For each valid move, we add the probability of reaching `(x, y)` by dividing the probability of reaching the previous position by `8` (since there are 8 possible moves).

3. **Final Calculation**:
   - After `k` moves, we sum all the probabilities for positions `(x, y)` that are within bounds on the chessboard to get the total probability.

## Time and Space Complexity:

- **Time Complexity**: O(k * n^2). 
  - We iterate over `k` moves, and for each move, we iterate over all `n^2` positions on the chessboard. For each position, we check 8 possible directions, which is constant.

- **Space Complexity**: O(k * n^2).
  - We store the probabilities in a 3D array `dp` with dimensions `(k + 1) x n x n`.

## Example Walkthrough:

Consider the input `n = 3`, `k = 2`, `row = 0`, `column = 0`.

1. **Initialization**:
   - `dp[0][0][0] = 1` because the knight starts at position `(0, 0)`.

2. **After 1 Move**:
   - The knight can move to positions `(2, 1)`, `(1, 2)`, and `(1, -2)` (among others).
   - Update probabilities based on previous positions.

3. **After 2 Moves**:
   - Continue updating probabilities based on the knight’s moves and previous steps.

4. **Final Answer**:
   - Sum the probabilities of all positions on the board after `2` moves.

Thus, the probability of the knight remaining on the board after `2` moves is `0.0625`.

## Conclusion

This dynamic programming approach efficiently computes the probability of a knight remaining on the board after `k` moves. The time complexity is O(k * n^2), making it feasible for the given constraints.