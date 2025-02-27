# Solution to "1730. Shortest Path to Get Food"

## Problem Statement

You are given an `m x n` grid where:

- Each cell can be:
    - `'*'`: Your location.
    - `'#'`: A food cell.
    - `'O'`: An empty cell.
    - `'X'`: An obstacle.
- You can move up, down, left, or right.

Return the length of the shortest path from your location to a food cell. If no path exists, return `-1`.

---

## Approach: Breadth-First Search (BFS)

### Explanation

We use a Breadth-First Search (BFS) approach to find the shortest path:

1. Start from the cell marked `'*'` (your location).
2. Use a queue to explore the grid level by level.
3. Move in all four possible directions (up, down, left, right).
4. If a food cell (`'#'`) is found, return the current distance.
5. If no path exists, return `-1`.

### Algorithm Steps

1. Find the starting cell `'*'`.
2. Initialize a queue with the start cell and a distance of `0`.
3. Perform BFS:
    - Dequeue the current cell.
    - If the cell is food (`'#'`), return the distance.
    - Explore neighbors and add them to the queue if they are valid (`'O'`).
4. If no food cell is reachable, return `-1`.

---

## Implementation in Python

```python
from collections import deque

class Solution:
    def getFood(self, grid: list[list[str]]) -> int:
        rows, cols = len(grid), len(grid[0])
        queue = deque()

        # Find the start location '*'
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '*':
                    queue.append((r, c, 0))  # (row, col, distance)
                    break

        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        while queue:
            r, c, dist = queue.popleft()

            if grid[r][c] == '#':
                return dist

            # Mark cell as visited
            grid[r][c] = 'X'

            # Explore neighbors
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] in ('O', '#'):
                    queue.append((nr, nc, dist + 1))

        return -1
```

---

## Example Run

Input:

```python
grid = [
    ['X', 'X', 'X', 'X', 'X', 'X'],
    ['X', '*', 'O', 'O', 'O', 'X'],
    ['X', 'O', 'O', '#', 'O', 'X'],
    ['X', 'X', 'X', 'X', 'X', 'X']
]

solution = Solution()
print(solution.getFood(grid))
```

Output:

```
3
```

Explanation:

- The shortest path is `'*' → 'O' → 'O' → '#'` with length `3`.

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Each cell is visited at most once.
2. **Space Complexity:** `O(m * n)`
    
    - Queue size can grow to the number of cells.

---

## Edge Cases

1. No food cell reachable → Output `-1`.
2. Start cell is next to food → Output `1`.

---

## Conclusion

This solution efficiently finds the shortest path to food using a breadth-first search approach while ensuring optimal time complexity.