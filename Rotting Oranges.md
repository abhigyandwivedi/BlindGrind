# Solution to "994. Rotting Oranges"

## Problem Statement

Given a grid of oranges, where:

- `0` represents an empty cell,
- `1` represents a fresh orange, and
- `2` represents a rotten orange,

Every minute, any fresh orange adjacent (up, down, left, right) to a rotten one also becomes rotten. Return the minimum number of minutes until no fresh orange remains. If it's impossible, return `-1`.

Example:

```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4

Input: grid = [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
```

---

## Approach: Breadth-First Search (BFS)

### Explanation

1. **Multi-Source BFS:** Start from all rotten oranges simultaneously.
2. **Queue Processing:** Use a queue to track rotten oranges and process them level by level (minute by minute).
3. **Count Fresh Oranges:** If any fresh oranges remain after processing, return `-1`.

---

## Implementation in Python

```python
from collections import deque

def orangesRotting(grid):
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0

    # Initialize queue with all rotten oranges and count fresh oranges
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                queue.append((r, c, 0))  # (row, col, minute)
            elif grid[r][c] == 1:
                fresh += 1

    # BFS to rot adjacent oranges
    minutes = 0
    directions = [(1, 0), (0, 1), (-1, 0), (0, -1)]

    while queue:
        r, c, minutes = queue.popleft()
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                fresh -= 1
                queue.append((nr, nc, minutes + 1))

    return minutes if fresh == 0 else -1

# Example usage
grid = [[2,1,1],[1,1,0],[0,1,1]]
result = orangesRotting(grid)
print(result)
```

---

## Example Run

Input:

```python
grid = [[2,1,1],[1,1,0],[0,1,1]]
result = orangesRotting(grid)
print(result)
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)`
    
    - Every cell is processed once.
2. **Space Complexity:** `O(m * n)`
    
    - Queue holds all rotten oranges at once.

---

## Edge Cases

1. No fresh oranges: Return `0`.
2. All oranges isolated: Return `-1`.
3. Single fresh with no rotten nearby: Return `-1`.

---

## Conclusion

This solution efficiently finds the minimum time to rot all oranges using multi-source BFS, ensuring correctness for all cases.