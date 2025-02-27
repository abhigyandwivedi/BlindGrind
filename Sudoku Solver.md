# LeetCode 37: Sudoku Solver

## Problem Statement

Write a program to solve a Sudoku puzzle by filling the empty cells. A Sudoku solution must satisfy the following conditions:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes must contain the digits `1-9` without repetition.

The given board is partially filled, and you need to fill the rest of the board in-place.

---

## Example

### Example Input

```
Input:
board =
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
```

### Example Output

```
Output:
[
  ["5","3","4","6","7","8","9","1","2"],
  ["6","7","2","1","9","5","3","4","8"],
  ["1","9","8","3","4","2","5","6","7"],
  ["8","5","9","7","6","1","4","2","3"],
  ["4","2","6","8","5","3","7","9","1"],
  ["7","1","3","9","2","4","8","5","6"],
  ["9","6","1","5","3","7","2","8","4"],
  ["2","8","7","4","1","9","6","3","5"],
  ["3","4","5","2","8","6","1","7","9"]
]
```

---

## Approach

We can solve the Sudoku puzzle using **backtracking** with optimization. The approach involves the following steps:

### Steps:

1. **Find Empty Cell:** Identify the first empty cell (denoted by `.`).
2. **Try Numbers:** Try placing digits `1-9` in the empty cell.
3. **Check Validity:** Ensure the current placement is valid (row, column, and 3x3 sub-box).
4. **Use Hash Sets:** Use row, column, and sub-box hash sets to track the numbers already used.
5. **Recursive Backtracking:** If the placement is valid, recursively solve the next cell.
6. **Backtrack if Needed:** If placing any number leads to a dead end, backtrack by resetting the cell to `.`.
7. **Repeat:** Continue until the board is completely filled.

---

## Solution (Python)

```python
def solveSudoku(board):
    rows = [set() for _ in range(9)]
    cols = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]

    # Initialize the sets with existing numbers
    for i in range(9):
        for j in range(9):
            if board[i][j] != '.':
                num = board[i][j]
                rows[i].add(num)
                cols[j].add(num)
                boxes[(i // 3) * 3 + (j // 3)].add(num)

    def backtrack(row=0, col=0):
        if row == 9:
            return True
        if col == 9:
            return backtrack(row + 1, 0)
        if board[row][col] != '.':
            return backtrack(row, col + 1)

        box_index = (row // 3) * 3 + (col // 3)
        for num in map(str, range(1, 10)):
            if num not in rows[row] and num not in cols[col] and num not in boxes[box_index]:
                board[row][col] = num
                rows[row].add(num)
                cols[col].add(num)
                boxes[box_index].add(num)

                if backtrack(row, col + 1):
                    return True

                # Backtrack
                board[row][col] = '.'
                rows[row].remove(num)
                cols[col].remove(num)
                boxes[box_index].remove(num)

        return False

    backtrack()
```

---

## Detailed Explanation

1. **Data Structures:**
    
    - `rows[i]`: Set of numbers present in the `i-th` row.
    - `cols[j]`: Set of numbers present in the `j-th` column.
    - `boxes[k]`: Set of numbers present in the `k-th` 3x3 sub-box.
2. **Initialization:**
    
    - Iterate through the board and populate the hash sets with existing numbers.
3. **Backtracking:**
    
    - Find an empty cell, try numbers `1-9`, and check if they're valid using the sets.
    - If valid, place the number, update sets, and recursively solve.
    - If no solution is found, backtrack by resetting the cell and removing the number from sets.
4. **Base Case:**
    
    - If all cells are filled (`row == 9`), the board is solved, and the recursion ends.

---

## Complexity Analysis

### Time Complexity: O(9^M)

- `M` is the number of empty cells.
- Each cell has 9 possibilities, but the hash sets significantly reduce invalid checks.

### Space Complexity: O(81) = O(1)

- The additional space is used for the hash sets (`rows`, `cols`, `boxes`), each storing at most 9 elements per row, column, and box.

---

## Edge Cases

1. **Already Solved Sudoku:** It should return immediately without changes.
2. **Invalid Sudoku Input:** If unsolvable, the board remains unchanged.
3. **Multiple Solutions:** The code finds one valid solution, not all.

---

## Example Run

For the input example, the output will be:

```
[
  ["5","3","4","6","7","8","9","1","2"],
  ["6","7","2","1","9","5","3","4","8"],
  ["1","9","8","3","4","2","5","6","7"],
  ["8","5","9","7","6","1","4","2","3"],
  ["4","2","6","8","5","3","7","9","1"],
  ["7","1","3","9","2","4","8","5","6"],
  ["9","6","1","5","3","7","2","8","4"],
  ["2","8","7","4","1","9","6","3","5"],
  ["3","4","5","2","8","6","1","7","9"]
]
```

---

## Conclusion

This optimized solution solves the Sudoku puzzle efficiently using backtracking with hash sets. It explores valid paths while pruning invalid ones, significantly improving performance compared to naive backtracking.