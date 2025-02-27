# Solution to "323. Number of Connected Components in an Undirected Graph"

## Problem Statement

Given `n` nodes labeled from `0` to `n - 1` and a list of `edges`, write a function to find the number of connected components in an undirected graph.

---

## Approach: Union-Find (Disjoint Set Union)

### Explanation

We can efficiently solve this problem using the Union-Find data structure to group connected components.

### Algorithm Steps

1. **Initialization:**
    
    - Create a parent array where each node is its own parent.
2. **Union Operation:**
    
    - For each edge `(u, v)`, merge the sets containing `u` and `v`.
3. **Find Operation:**
    
    - Find the root parent of each node using path compression.
4. **Count Components:**
    
    - Count unique roots to determine the number of connected components.

---

## Implementation in Python

```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        parent = [i for i in range(n)]

        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])  # Path compression
            return parent[x]

        def union(x, y):
            root_x = find(x)
            root_y = find(y)
            if root_x != root_y:
                parent[root_x] = root_y

        # Process each edge
        for u, v in edges:
            union(u, v)

        # Count unique roots
        unique_roots = len(set(find(i) for i in range(n)))
        return unique_roots
```

---

## Example Run

Input:

```python
n = 5
edges = [[0, 1], [1, 2], [3, 4]]
solution = Solution()
print(solution.countComponents(n, edges))
```

Output:

```
2
```

---

## Complexity Analysis

1. **Time Complexity:** `O(E α(N))`
    
    - `E` is the number of edges, and `α(N)` is the inverse Ackermann function (almost constant).
2. **Space Complexity:** `O(N)`
    
    - Extra space for the parent array.

---

## Edge Cases

1. No edges → `n` connected components.
2. Fully connected graph → 1 connected component.
3. Disconnected nodes → Each node is its own component.

---

## Conclusion

This solution efficiently finds the number of connected components using the Union-Find approach, achieving near-linear time complexity.