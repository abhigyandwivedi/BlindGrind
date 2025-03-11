  1490 Clone N-ary tree
  # Clone N-ary Tree

## Problem Statement

Given the root of an N-ary tree, create a deep copy (clone) of the tree. Each node in the N-ary tree contains a `val` and a list of children.

## Approach

1. Use Depth-First Search (DFS) or Breadth-First Search (BFS) to traverse the tree.
2. Create a new node for each node encountered and recursively copy its children.
3. Maintain a mapping to avoid duplicate copies.

## Code Implementation (Python)

### Recursive DFS Approach

```python
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children if children is not None else []

def cloneTree(root: 'Node') -> 'Node':
    if not root:
        return None
    
    new_root = Node(root.val)
    for child in root.children:
        new_root.children.append(self.cloneTree(child))
    
    return new_root
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In the worst case (skewed tree), **O(N)** space is required.
- For a balanced tree, **O(log N)** space is used.

## Alternative Approach: Iterative BFS Using Queue

Instead of recursion, we can use a queue to perform a level-order traversal and clone nodes iteratively:

```python
from collections import deque

def cloneTree_bfs(root: 'Node') -> 'Node':
    if not root:
        return None
    
    mapping = {}
    queue = deque([root])
    
    mapping[root] = Node(root.val)
    
    while queue:
        node = queue.popleft()
        
        for child in node.children:
            if child not in mapping:
                mapping[child] = Node(child.val)
                queue.append(child)
            mapping[node].children.append(mapping[child])
    
    return mapping[root]
```

### Complexity of BFS Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(N)** (hashmap stores `N` nodes in the worst case)

## Conclusion

Both recursive and iterative approaches efficiently clone an N-ary tree. The recursive method is simpler, while the BFS approach avoids recursion depth issues and is more memory-efficient in balanced trees.