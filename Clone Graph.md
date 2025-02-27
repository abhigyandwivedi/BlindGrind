# Solution to "133. Clone Graph"

## Problem Statement

Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a `val` (int) and a list of `neighbors` (List[Node]).

Example:

```
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: A deep copy of the graph.
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Use a HashMap:** Create a map to store cloned nodes.
2. **DFS Traversal:** For each node, recursively clone its neighbors.
3. **Avoid Cycles:** Use the hashmap to avoid re-cloning visited nodes.

---

## Implementation in Python

```python
class Node:
    def __init__(self, val=0, neighbors=None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []

def cloneGraph(node):
    if not node:
        return None

    old_to_new = {}

    def dfs(node):
        if node in old_to_new:
            return old_to_new[node]

        clone = Node(node.val)
        old_to_new[node] = clone
        for neighbor in node.neighbors:
            clone.neighbors.append(dfs(neighbor))
        
        return clone

    return dfs(node)

# Example usage
# Assuming graph nodes are properly defined elsewhere
```

---

## Complexity Analysis

1. **Time Complexity:** `O(V + E)` where `V` is the number of vertices and `E` is the number of edges.
2. **Space Complexity:** `O(V)` for storing cloned nodes and recursion stack.

---

## Example Run

Input:

```
Node 1 with neighbors [2, 4]
Node 2 with neighbors [1, 3]
Node 3 with neighbors [2, 4]
Node 4 with neighbors [1, 3]
```

Output:

```
Cloned graph with the same structure.
```

---

## Edge Cases

1. Empty graph: `None` → Output: `None`
2. Single node: Node with no neighbors → Output: Cloned single node

---

## Conclusion

This solution efficiently clones an undirected graph using DFS and a hashmap to avoid cycles and redundant work.