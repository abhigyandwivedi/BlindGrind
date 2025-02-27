# Solution to "542. 01 Matrix"

## Problem Statement

Given an `m x n` binary matrix `mat`, return the distance of the nearest `0` for each cell.

The distance between two adjacent cells is `1`.

Example:

```
Input: mat = [
 [0,0,0],
 [0,1,0],
 [1,1,1]
]
Output: [
 [0,0,0],
 [0,1,0],
 [1,2,1]
]
```

---

## Approach: Breadth-First Search (BFS)

### Explanation

1. **Initialization:** Create a queue and initialize all `0` cells in the queue while marking `1` cells as `inf`.
2. **BFS Traversal:** Start from each `0` cell and update neighboring `1` cells with the shortest distance.
3. **Result:** After the BFS traversal, each cell contains the distance to the nearest `0`.

---

## Implementation in Python

```python
from collections import deque

def updateMatrix(mat):
    rows, cols = len(mat), len(mat[0])
    queue = deque()
    
    # Initialize queue with all 0 cells and mark 1 cells as infinity
    for r in range(rows):
        for c in range(cols):
            if mat[r][c] == 0:
                queue.append((r, c))
            else:
                mat[r][c] = float('inf')
    
    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
    
    # BFS to update distances
    while queue:
        r, c = queue.popleft()
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and mat[nr][nc] > mat[r][c] + 1:
                mat[nr][nc] = mat[r][c] + 1
                queue.append((nr, nc))
    
    return mat

# Example usage
mat = [
    [0,0,0],
    [0,1,0],
    [1,1,1]
]
print(updateMatrix(mat))
```

---

## Complexity Analysis

1. **Time Complexity:** `O(m * n)` - Each cell is processed once during the BFS traversal.
2. **Space Complexity:** `O(m * n)` - Queue storage for all cells.

---

## Example Run

Input:

```
mat = [
 [0,0,0],
 [0,1,0],
 [1,1,1]
]
```

Output:

```
[
 [0,0,0],
 [0,1,0],
 [1,2,1]
]
```

---

## Edge Cases

1. All cells are `0` → Output remains the same.
2. All cells are `1` → Each cell gets the distance to the nearest boundary `0`.
3. Single row/column → Handled similarly with BFS propagation.

---

## Conclusion

This solution efficiently computes the shortest distance to the nearest `0` using a multi-source BFS approach, ensuring optimal time and space complexity.