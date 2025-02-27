# Solution to "51. N-Queens"

## Problem Statement

The N-Queens puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Example:

```
Input: n = 4
Output:
[
 [".Q..",
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",
  "Q...",
  "...Q",
  ".Q.."]
]
```

---

## Approach: Backtracking

### Explanation

1. **Backtracking:** Place queens row by row and backtrack if conflicts occur.
2. **Conflict Check:** Ensure no two queens share the same column, major diagonal, or minor diagonal.
3. **Base Case:** If `n` queens are placed, add the board configuration to the result.

---

## Implementation in Python

```python
def solveNQueens(n):
    def backtrack(row, cols, diagonals1, diagonals2, board):
        if row == n:
            result.append(["".join(row) for row in board])
            return
        
        for col in range(n):
            if col in cols or (row - col) in diagonals1 or (row + col) in diagonals2:
                continue

            board[row][col] = 'Q'
            cols.add(col)
            diagonals1.add(row - col)
            diagonals2.add(row + col)

            backtrack(row + 1, cols, diagonals1, diagonals2, board)

            board[row][col] = '.'
            cols.remove(col)
            diagonals1.remove(row - col)
            diagonals2.remove(row + col)

    result = []
    board = [['.'] * n for _ in range(n)]
    backtrack(0, set(), set(), set(), board)
    return result

# Example usage
n = 4
solutions = solveNQueens(n)
for solution in solutions:
    for row in solution:
        print(row)
    print()
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n!)` - In the worst case, we explore all permutations of queens.
2. **Space Complexity:** `O(n^2)` - For storing the board and recursion stack.

---

## Example Run

Input:

```
n = 4
```

Output:

```
.Q..
...Q
Q...
..Q.

..Q.
Q...
...Q
.Q..
```

---

## Edge Cases

1. `n = 1` returns `["Q"]`.
2. `n = 2` or `n = 3` returns an empty list (no solutions).

---

## Conclusion

This solution efficiently finds all valid N-Queens placements using backtracking while avoiding conflicts.