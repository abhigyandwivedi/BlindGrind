# Solution to "79. Word Search"

## Problem Statement

Given an `m x n` board and a word, find if the word exists in the grid. The word can be constructed from sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same cell cannot be used more than once.

Example:

```
Input: board = [
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
], word = "ABCCED"
Output: true
```

---

## Approach: Backtracking

### Explanation

1. **DFS Traversal:** Start from each cell and perform depth-first search.
2. **Recursive Search:** Check if the current cell matches the next character of the word.
3. **Mark Visited:** Temporarily mark cells as visited to avoid reuse.
4. **Backtrack:** Revert the cell state after exploring all possibilities.

---

## Implementation in Python

```python
def exist(board, word):
    rows, cols = len(board), len(board[0])

    def dfs(r, c, index):
        if index == len(word):
            return True
        if r < 0 or r >= rows or c < 0 or c >= cols or board[r][c] != word[index]:
            return False

        # Mark the cell as visited
        temp, board[r][c] = board[r][c], '#'

        # Explore all directions
        found = (dfs(r + 1, c, index + 1) or
                 dfs(r - 1, c, index + 1) or
                 dfs(r, c + 1, index + 1) or
                 dfs(r, c - 1, index + 1))

        # Restore the cell state
        board[r][c] = temp
        return found

    for i in range(rows):
        for j in range(cols):
            if board[i][j] == word[0] and dfs(i, j, 0):
                return True

    return False
```

---

## Example Run

Input:

```python
board = [
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
word = "ABCCED"
print(exist(board, word))  # Output: True
```

Output:

```
True
```

Explanation:

- The word "ABCCED" is found by traversing `board[0][0] -> board[0][1] -> board[0][2] -> board[1][2] -> board[1][1] -> board[2][1]`.

---

## Complexity Analysis

1. **Time Complexity:** `O(M * N * 4^L)`
    
    - `M * N` for traversing the board.
    - `4^L` for exploring each word path (`L` is the word length).
2. **Space Complexity:** `O(L)`
    
    - Recursive call stack depth based on the word length.

---

## Edge Cases

1. If the board is empty, return `False`.
2. If the word is empty, return `True`.

---

## Conclusion

This backtracking approach efficiently searches for the word while ensuring cells are not reused.