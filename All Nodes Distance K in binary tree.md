# 863. All Nodes Distance K in Binary Tree

## Problem Statement

Given the `root` of a binary tree, a target node, and an integer `k`, return all the values of nodes that are exactly `k` distance away from the target node.

### Example

**Input:**

```
root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, k = 2
```

**Output:**

```
[7, 4, 1]
```

**Explanation:** The nodes 7, 4, and 1 are at distance 2 from the target node 5.

---

## Approach: Graph Traversal (BFS)

### Idea

1. Treat the binary tree as an undirected graph.
2. Convert the tree into a graph where each node points to its children and parent.
3. Perform a breadth-first search (BFS) starting from the target node and move `k` levels away.

---

## Implementation (Python)

```python
from collections import defaultdict, deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def distanceK(root, target, k):
    graph = defaultdict(list)

    # Build graph from the binary tree
    def build_graph(node, parent=None):
        if not node:
            return
        if parent:
            graph[node.val].append(parent.val)
            graph[parent.val].append(node.val)
        build_graph(node.left, node)
        build_graph(node.right, node)

    build_graph(root)

    # Perform BFS from the target node
    queue = deque([(target.val, 0)])
    visited = set([target.val])
    result = []

    while queue:
        node, distance = queue.popleft()
        if distance == k:
            result.append(node)
        if distance > k:
            break
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append((neighbor, distance + 1))

    return result
```

---

## Example Run

For `root = [3,5,1,6,2,0,8,null,null,7,4]`, `target = 5`, and `k = 2`:

1. Build the graph:

```
3: [5, 1]
5: [3, 6, 2]
1: [3, 0, 8]
6: [5]
2: [5, 7, 4]
0: [1]
8: [1]
7: [2]
4: [2]
```

1. Perform BFS from node `5`.
2. Nodes at distance `2` are `[7, 4, 1]`.

Output: `[7, 4, 1]`

---

## Complexity Analysis

### Time Complexity

- **O(N):** Each node and edge is processed once.

### Space Complexity

- **O(N):** Graph storage and BFS queue.

---

## Edge Cases

1. `k = 0` → Output: `[target.val]` (Only the target node itself).
2. `k > height of tree` → Output: `[]` (No nodes at that distance).
3. Single node tree → Output depends on `k` value.

---

## Conclusion

This solution efficiently finds all nodes at distance `k` from the target node using graph traversal, ensuring linear time complexity relative to the size of the tree.