# LeetCode 212: Word Search II Solution

## Problem Statement

Given an `m x n` board of characters and a list of strings `words`, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where "adjacent" cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

---

## Approach: Trie and Backtracking

To efficiently find all words, we use a combination of a **Trie (prefix tree)** and **backtracking**. This approach allows us to prune unnecessary searches and avoid checking each word independently.

### Explanation

1. **Trie Construction:**
    
    - Insert all words into a Trie. This helps in quickly checking if a path on the board is a prefix of any word.
2. **Backtracking:**
    
    - Start DFS from each cell of the board.
    - Explore each valid neighboring cell.
    - If a word is found (i.e., the end of a word in the Trie), add it to the result.
    - Use a visited marker to avoid revisiting cells.
3. **Pruning:**
    
    - If a path doesn't lead to any word, backtrack immediately.
    - Once a word is found, remove it from the Trie to prevent duplicate searches.

---

## Implementation in Python

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False
        self.word = None

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
        node.word = word

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        def backtrack(row, col, parent):
            letter = board[row][col]
            curr_node = parent.children[letter]

            # Found a word
            if curr_node.is_end_of_word:
                result.add(curr_node.word)
                curr_node.is_end_of_word = False

            # Mark the cell as visited
            board[row][col] = "#"

            # Explore neighbors
            for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                nr, nc = row + dr, col + dc
                if 0 <= nr < len(board) and 0 <= nc < len(board[0]) and board[nr][nc] in curr_node.children:
                    backtrack(nr, nc, curr_node)

            # Restore the cell
            board[row][col] = letter

            # Optimization: Prune the Trie
            if not curr_node.children:
                parent.children.pop(letter)

        # Build Trie
        trie = Trie()
        for word in words:
            trie.insert(word)

        result = set()

        # Start backtracking from each cell
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] in trie.root.children:
                    backtrack(i, j, trie.root)

        return list(result)
```

---

## Example Run

Input:

```python
board = [
    ['o', 'a', 'a', 'n'],
    ['e', 't', 'a', 'e'],
    ['i', 'h', 'k', 'r'],
    ['i', 'f', 'l', 'v']
]
words = ["oath", "pea", "eat", "rain"]
s = Solution()
print(s.findWords(board, words))
```

Output:

```
['oath', 'eat']
```

---

## Complexity Analysis

### Time Complexity

1. **Trie Construction:** O(L)O(L), where LL is the total number of characters across all words.
2. **Backtracking:** For each cell, in the worst case, we explore all paths, leading to O(mn⋅4L)O(mn \cdot 4^L), where:
    - m×nm \times n is the board size.
    - 4L4^L represents four directions for a word of length LL.

However, Trie pruning significantly reduces unnecessary exploration.

### Space Complexity

1. **Trie Storage:** O(L)O(L) for storing all words.
2. **Recursion Stack:** O(L)O(L) for the backtracking stack depth.

Total space complexity: O(L+mn)O(L + mn).

---

## Optimizations

1. **Early Exit:** Stop exploring paths when no prefix exists in the Trie.
2. **Trie Pruning:** Remove nodes from the Trie after finding a word.
3. **Visited Marker:** Use an in-place marker (`#`) instead of an extra visited array.

---

## Conclusion

This solution efficiently finds all words in the board using Trie and backtracking. The pruning strategy ensures reduced search space and improved performance compared to brute-force approaches.