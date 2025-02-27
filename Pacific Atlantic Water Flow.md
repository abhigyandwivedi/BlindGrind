# Solution to "417. Pacific Atlantic Water Flow"

## Problem Statement

Given an `m x n` matrix of heights representing the height of each cell, return a list of grid coordinates where water can flow to both the Pacific and Atlantic oceans.

- Water can only flow from higher or equal heights to lower heights.
- The Pacific ocean touches the left and top edges of the matrix.
- The Atlantic ocean touches the right and bottom edges.

---

## Approach: Depth-First Search (DFS)

### Explanation

We perform two Depth-First Search (DFS) traversals:

1. From cells adjacent to the Pacific Ocean (top and left borders).
2. From cells adjacent to the Atlantic Ocean (bottom and right borders).

We mark cells reachable from each ocean and find the intersection of these sets.

### Algorithm Steps

1. Create two sets: `pacific_reachable` and `atlantic_reachable`.
2. Perform DFS from the Pacific border and Atlantic border.
3. Collect cells reachable from both oceans.

---

## Implementation in Python

```python
class Solution:
    def pacificAtlantic(self, heights: list[list[int]]) -> list[list[int]]:
        if not heights or not heights[0]:
            return []

        rows, cols = len(heights), len(heights[0])
        pacific_reachable = set()
        atlantic_reachable = set()

        def dfs(r, c, reachable, prev_height):
            if (
                r < 0 or c < 0 or r >= rows or c >= cols
                or (r, c) in reachable
                or heights[r][c] < prev_height
            ):
                return

            reachable.add((r, c))
            for dr, dc in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                dfs(r + dr, c + dc, reachable, heights[r][c])

        # Run DFS from Pacific and Atlantic borders
        for r in range(rows):
            dfs(r, 0, pacific_reachable, heights[r][0])  # Pacific left
            dfs(r, cols - 1, atlantic_reachable, heights[r][cols - 1])  # Atlantic right
        for c in range(cols):
            dfs(0, c, pacific_reachable, heights[0][c])  # Pacific top
            dfs(rows - 1, c, atlantic_reachable, heights[rows - 1][c])  # Atlantic bottom

        # Find intersection
        return list(pacific_reachable & atlantic_reachable)
```

---

## Example Run

Input:

```python
heights = [
    [1, 2, 2, 3, 5],
    [3, 2, 3, 4, 4],
    [2, 4, 5, 3, 1],
    [6, 7, 1, 4, 5],
    [5, 1, 1, 2, 4]
]

solution = Solution()
print(solution.pacificAtlantic(heights))
```

Output:

```
[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]]
```

Explanation:

- These cells can flow to both the Pacific and Atlantic oceans.

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Each cell is visited once for both oceans.
2. **Space Complexity:** `O(m * n)`
    
    - To store the reachable cells.

---

## Edge Cases

1. Empty matrix → Output `[]`.
2. Single row or column → All cells reachable.

---

## Conclusion

This solution efficiently finds cells where water can flow to both oceans using DFS while ensuring optimal time complexity.