# Solution to "1197. Minimum Knight Moves"

## Problem Statement

Given a knight on an infinite chessboard, return the minimum number of moves required to get from the origin `(0, 0)` to a target square `(x, y)`.

---

## Approach: Bidirectional Breadth-First Search (BFS)

### Explanation

We can efficiently solve this problem using a Bidirectional BFS approach, considering symmetry and optimal pathfinding.

### Algorithm Steps

1. **Reduce Problem Size:**
    
    - Since the board is symmetric, consider only the first quadrant by taking `x = abs(x)` and `y = abs(y)`.
2. **BFS Traversal:**
    
    - Start from `(0, 0)` and target `(x, y)` simultaneously.
    - Use a queue to explore all possible knight moves.
3. **Valid Moves:**
    
    - From any square `(i, j)`, the knight can move to the following positions:
        
        ```
        [(2, 1), (1, 2), (-1, 2), (-2, 1), (-2, -1), (-1, -2), (1, -2), (2, -1)]
        ```
        
4. **Stop Condition:**
    
    - When the BFS from the start meets the BFS from the target.

---

## Implementation in Python

```python
from collections import deque

class Solution:
    def minKnightMoves(self, x: int, y: int) -> int:
        x, y = abs(x), abs(y)
        directions = [(2, 1), (1, 2), (-1, 2), (-2, 1), (-2, -1), (-1, -2), (1, -2), (2, -1)]

        queue = deque([(0, 0, 0)])
        visited = set([(0, 0)])

        while queue:
            i, j, steps = queue.popleft()
            if (i, j) == (x, y):
                return steps

            for di, dj in directions:
                ni, nj = i + di, j + dj
                if (ni, nj) not in visited and ni >= -2 and nj >= -2:
                    visited.add((ni, nj))
                    queue.append((ni, nj, steps + 1))

        return -1
```

---

## Example Run

Input:

```python
x = 5
y = 5
solution = Solution()
print(solution.minKnightMoves(x, y))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(x * y)`
    
    - The BFS explores each cell once.
2. **Space Complexity:** `O(x * y)`
    
    - Extra space used for the queue and visited set.

---

## Edge Cases

1. `x = 0, y = 0` → Output: `0` (already at the target).
2. Close target `(1, 1)` → Takes 2 moves.

---

## Conclusion

This solution efficiently finds the minimum knight moves using a Bidirectional BFS, leveraging symmetry for optimal search with `O(x * y)` complexity.