# Solution to "310. Minimum Height Trees"

## Problem Statement

Given a tree with `n` nodes labeled from `0` to `n - 1`, find all the roots that produce minimum height trees. You are given an array `edges` where `edges[i] = [a, b]` indicates an undirected edge between node `a` and node `b`.

Example:

```
Input: n = 6, edges = [[0, 1], [1, 2], [1, 3], [2, 4], [3, 5]]
Output: [1]
```

---

## Approach: Topological Sort (BFS)

### Explanation

1. **Graph Construction:** Build an adjacency list for the graph.
2. **Leaf Node Identification:** Start with leaf nodes (degree = 1).
3. **Layered Removal:** Perform BFS, removing leaf nodes layer by layer.
4. **End Condition:** The remaining nodes are the roots of the Minimum Height Trees.

---

## Implementation in Python

```python
from collections import deque

def findMinHeightTrees(n, edges):
    if n == 1:
        return [0]

    # Build graph
    graph = [set() for _ in range(n)]
    for u, v in edges:
        graph[u].add(v)
        graph[v].add(u)

    # Initialize leaves
    leaves = deque([i for i in range(n) if len(graph[i]) == 1])

    # Trim leaves until 1 or 2 nodes remain
    remaining_nodes = n
    while remaining_nodes > 2:
        leaf_count = len(leaves)
        remaining_nodes -= leaf_count

        for _ in range(leaf_count):
            leaf = leaves.popleft()
            neighbor = graph[leaf].pop()
            graph[neighbor].remove(leaf)
            if len(graph[neighbor]) == 1:
                leaves.append(neighbor)

    return list(leaves)
```

---

## Example Run

Input:

```python
n = 6
edges = [[0, 1], [1, 2], [1, 3], [2, 4], [3, 5]]
print(findMinHeightTrees(n, edges))  # Output: [1]
```

Output:

```
[1]
```

Explanation:

- Node `1` serves as the root that produces the minimum height tree.

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - Constructing the graph takes `O(N)` time.
    - Removing leaf nodes takes `O(N)` time as each node is processed once.
2. **Space Complexity:** `O(N)`
    
    - Adjacency list and queue storage for nodes.

---

## Edge Cases

1. If `n = 1`, the result is `[0]`.
2. If the graph is already balanced, multiple roots may exist.

---

## Conclusion

This approach efficiently finds the roots of Minimum Height Trees by iteratively removing leaf nodes, ensuring optimal tree height.