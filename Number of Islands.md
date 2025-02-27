# Solution to "200. Number of Islands"

## Problem Statement

Given an `m x n` grid of `1`s (land) and `0`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are surrounded by water.

Example:

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Traverse the Grid:** Iterate through each cell in the grid.
2. **DFS on Land Cells:** If a cell is land (`1`), initiate a DFS to mark all connected land cells as visited.
3. **Count Islands:** Each DFS call represents one island.

---

## Implementation in Python

```python
def numIslands(grid):
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    visited = set()

    def dfs(r, c):
        if (r < 0 or r >= rows or c < 0 or c >= cols or
                grid[r][c] == "0" or (r, c) in visited):
            return
        visited.add((r, c))
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    count = 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == "1" and (r, c) not in visited:
                dfs(r, c)
                count += 1

    return count

# Example usage
grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
result = numIslands(grid)
print(result)
```

---

## Example Run

Input:

```python
grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
result = numIslands(grid)
print(result)
```

Output:

```
3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Each cell is visited once during the DFS traversal.
2. **Space Complexity:** `O(m * n)`
    
    - In the worst case, the recursion stack and visited set can grow to cover all cells.

---

## Edge Cases

1. Empty grid: Return `0`.
2. All water: Return `0`.
3. Single cell island: Return `1`.

---

## Conclusion

This solution efficiently finds the number of islands using a depth-first search approach, ensuring correctness across all cases.