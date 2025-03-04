#recursiongraph #union #unionfind #matrix
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


# Number of Islands (LeetCode 200) Union Find solution
## Problem Statement

You are given an `m x n` grid filled with `'1'` (land) and `'0'` (water). An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are surrounded by water.

Return the number of islands.

### Example 1:

```plaintext
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]

Output: 1
```

### Example 2:

```plaintext
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]

Output: 3
```

---

## Solution using Union-Find (Disjoint Set Union - DSU)

### Explanation

The **Union-Find (Disjoint Set)** data structure is well suited for problems related to connected components. In this problem, each cell in the grid can be seen as a node in a graph, and adjacent land cells should be connected.

The key idea is:

- Treat each land cell (`'1'`) as a separate node.
- Use **Union-Find** to merge adjacent land nodes into a single connected component.
- The number of unique roots in the Union-Find structure at the end represents the number of islands.

### Algorithm Steps:

1. **Initialize Union-Find**: Create a `parent` array where each land cell is its own parent.
2. **Iterate through the grid**:
    - If a cell contains `'1'`, process its right and bottom neighbors to union adjacent land cells.
    - Keep track of the number of connected components.
3. **Find the number of islands**: Count unique parents in the Union-Find structure.

### Code Implementation (Python):

```python
class UnionFind:
    def __init__(self, grid):
        rows, cols = len(grid), len(grid[0])
        self.parent = {}
        self.rank = {}
        self.count = 0  # Number of islands
        
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    self.parent[(r, c)] = (r, c)
                    self.rank[(r, c)] = 0
                    self.count += 1

    def find(self, node):
        if self.parent[node] != node:
            self.parent[node] = self.find(self.parent[node])  # Path compression
        return self.parent[node]
    
    def union(self, node1, node2):
        root1 = self.find(node1)
        root2 = self.find(node2)
        
        if root1 != root2:
            if self.rank[root1] > self.rank[root2]:
                self.parent[root2] = root1
            elif self.rank[root1] < self.rank[root2]:
                self.parent[root1] = root2
            else:
                self.parent[root2] = root1
                self.rank[root1] += 1
            self.count -= 1  # Merge islands, so reduce count

class Solution(object):
    def numIslands(self, grid):
        if not grid or not grid[0]:
            return 0
        
        rows, cols = len(grid), len(grid[0])
        uf = UnionFind(grid)
        directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        
        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    for dr, dc in directions:
                        nr, nc = r + dr, c + dc
                        if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == '1':
                            uf.union((r, c), (nr, nc))
        
        return uf.count
# Example usage
grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"],
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"],
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","1","1","0","0"],
  ["0","1","0","1","1"],
]
solution=Solution()
result = solution.numIslands(grid)
print(result)
```

### Complexity Analysis

- **Finding and Union Operations**: Almost **O(1)** (using path compression and rank optimization).
- **Iterating through the Grid**: **O(m × n)**.
- **Total Time Complexity**: **O(m × n)**.
- **Space Complexity**: **O(m × n)** (for storing the parent and rank arrays).

### Why Use Union-Find?

- Efficient for connected component problems.
- Faster than DFS in cases where the grid is large and sparse.
- Avoids stack overflow issues that DFS might have in deep recursions.

### Alternative Approach

- **DFS/BFS**: Recursively mark visited land cells. However, DFS can be slower in large grids, while BFS requires additional queue space.

---

## Summary

- **Union-Find** is an efficient way to count islands.
- **Time Complexity is O(m × n)**, making it efficient for large grids.
- **Better than DFS for certain cases**, especially with large inputs.

This approach ensures that we efficiently track and merge islands, leading to an optimized solution for the **Number of Islands** problem on LeetCode.
### **Time and Space Complexity Analysis** of the Union-Find approach:

#### **Time Complexity**:

1. **Initializing the Union-Find structure**:
    
    - We iterate over the entire grid once to initialize the `parent`, `rank`, and `count` dictionaries.
    - This takes **O(m × n)**, where `m` is the number of rows and `n` is the number of columns.
2. **Processing each cell**:
    
    - We iterate over the entire grid again (O(m × n)) and check its 4 possible neighbors.
    - Each `union` operation involves two `find` operations.
    - Using **path compression**, each `find` operation has an amortized time complexity of **O(α(m × n))**, where α (Ackermann function inverse) is nearly constant (~4 for all practical cases).
3. **Union operations**:
    
    - Since we perform at most O(m × n) union operations, and each operation is nearly **O(1)** due to path compression, this results in **O(m × n α(m × n))**, which simplifies to **O(m × n)** in practice.

**Overall Time Complexity: O(m × n)**

---

#### **Space Complexity**:

1. **Union-Find Data Structures**:
    
    - The `parent` dictionary stores at most **O(m × n)** elements (one for each land cell).
    - The `rank` dictionary also stores at most **O(m × n)** elements.
2. **Recursive Stack (in `find`)**:
    
    - Path compression may cause a recursive stack depth of O(log(m × n)), but this is negligible.

**Overall Space Complexity: O(m × n)** (for storing parent and rank dictionaries)

---

### **Final Complexity Summary**:

|Operation|Time Complexity|Space Complexity|
|---|---|---|
|Initialization|O(m × n)|O(m × n)|
|Union-Find operations|O(m × n α(m × n)) ≈ O(m × n)|O(m × n)|
|**Total**|**O(m × n)**|**O(m × n)**|

This Union-Find approach is **efficient** compared to DFS/BFS, especially for large grids, as it avoids unnecessary recursion or queue operations. 🚀