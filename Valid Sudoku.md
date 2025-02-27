# Solution to "36. Valid Sudoku"

## Problem Statement

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes must contain the digits `1-9` without repetition.

---

## Approach: Hash Set for Validation

### Explanation

We use three sets:

1. `rows` to track digits in each row.
2. `cols` to track digits in each column.
3. `boxes` to track digits in each `3 x 3` box.

For each cell with a number, we:

1. Check if it exists in the corresponding row, column, or box.
2. If not, add it to the respective sets.

### Algorithm Steps

1. Iterate through each cell in the board.
2. Skip empty cells (`'.'`).
3. For each number, calculate its corresponding box index using:
    
    ```python
    box_index = (row // 3) * 3 + (col // 3)
    ```
    
4. Check if the number exists in the respective sets.
5. If any condition fails, return `False`.
6. If all cells are valid, return `True`.

---

## Implementation in Python

```python
class Solution:
    def isValidSudoku(self, board: list[list[str]]) -> bool:
        rows = [set() for _ in range(9)]
        cols = [set() for _ in range(9)]
        boxes = [set() for _ in range(9)]

        for i in range(9):
            for j in range(9):
                num = board[i][j]
                if num == '.':
                    continue

                box_index = (i // 3) * 3 + (j // 3)

                if (num in rows[i] or
                    num in cols[j] or
                    num in boxes[box_index]):
                    return False

                rows[i].add(num)
                cols[j].add(num)
                boxes[box_index].add(num)

        return True
```

---

## Example Run

Input:

```python
board = [
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
solution = Solution()
print(solution.isValidSudoku(board))
```

Output:

```
True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(81)` → `O(1)`
    
    - We iterate through all `81` cells.
2. **Space Complexity:** `O(81)` → `O(1)`
    
    - Storage for sets tracking rows, columns, and boxes.

---

## Edge Cases

1. Empty cells → Ignored.
2. Duplicate in any row, column, or box → Return `False`.
3. Valid board → Return `True`.

---

## Conclusion

This solution efficiently validates a Sudoku board using hash sets for rows, columns, and `3 x 3` boxes.