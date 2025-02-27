# Solution to "261. Graph Valid Tree"

## Problem Statement

Given `n` nodes labeled from `0` to `n - 1` and a list of `edges` where `edges[i] = [ai, bi]` indicates an undirected edge between nodes `ai` and `bi`, return `true` if these edges form a valid tree.

---

## Approach: Union-Find (Disjoint Set)

### Explanation

To determine if the graph forms a valid tree, we need to ensure two conditions:

1. **No cycles:** A tree cannot have cycles.
2. **Single connected component:** All nodes must be connected.

**Union-Find Approach:**

1. Initialize a parent array where each node is its own parent.
2. For each edge `(a, b)`, perform the following:
    - Find the root parent of both `a` and `b`.
    - If they have the same root, a cycle exists, so return `False`.
    - Otherwise, union the two nodes.
3. After processing all edges, check if the number of edges is `n - 1` (a tree with `n` nodes has exactly `n - 1` edges).

---

## Implementation in Python

```python
class Solution:
    def validTree(self, n: int, edges: list[list[int]]) -> bool:
        if len(edges) != n - 1:
            return False

        parent = [i for i in range(n)]

        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]

        def union(x, y):
            root_x = find(x)
            root_y = find(y)

            if root_x == root_y:
                return False

            parent[root_x] = root_y
            return True

        for a, b in edges:
            if not union(a, b):
                return False

        return True
```

---

## Example Run

Input:

```python
n = 5
edges = [[0, 1], [0, 2], [0, 3], [1, 4]]
solution = Solution()
print(solution.validTree(n, edges))
```

Output:

```
True
```

Explanation: The graph forms a valid tree with no cycles and all nodes connected.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each `find` and `union` operation takes nearly constant time with path compression.
2. **Space Complexity:** `O(n)`
    
    - To store the parent array.

---

## Edge Cases

1. Empty graph with `n = 1` → `True`.
2. Cycle exists → `False`.
3. Disconnected components → `False`.

---

## Conclusion

This solution efficiently checks whether an undirected graph forms a valid tree using the Union-Find approach, ensuring both acyclic structure and connectivity.