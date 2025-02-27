# 1315. Sum of Nodes with Even-Valued Grandparent

## Problem Statement

Given a binary tree, return the sum of values of all nodes whose grandparent has an even value.

- A grandparent of a node is the parent of its parent.
- The root node does not have a grandparent.

## Approach

1. Use Depth-First Search (DFS) to traverse the tree.
2. Keep track of the parent and grandparent of each node.
3. If the grandparent's value is even, add the node's value to the sum.
4. Recursively process the left and right children.

## Code Implementation (Python)

### Recursive Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def sumEvenGrandparent(root: TreeNode) -> int:
    def dfs(node, parent=None, grandparent=None):
        if not node:
            return 0
        
        total = 0
        if grandparent and grandparent.val % 2 == 0:
            total += node.val
        
        total += dfs(node.left, node, parent)
        total += dfs(node.right, node, parent)
        
        return total
    
    return dfs(root)
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.

## Alternative Approach: Iterative Using Queue (BFS)

Instead of recursion, we can use a queue for level-order traversal:

```python
from collections import deque

def sumEvenGrandparent_bfs(root: TreeNode) -> int:
    if not root:
        return 0
    
    queue = deque([(root, None, None)])
    total_sum = 0
    
    while queue:
        node, parent, grandparent = queue.popleft()
        
        if grandparent and grandparent.val % 2 == 0:
            total_sum += node.val
        
        if node.left:
            queue.append((node.left, node, parent))
        if node.right:
            queue.append((node.right, node, parent))
    
    return total_sum
```

### Complexity of BFS Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(N)** (queue holds nodes in worst case)

## Conclusion

Both DFS and BFS approaches efficiently compute the sum of nodes with even-valued grandparents. The DFS approach is more memory-efficient for balanced trees, while the BFS method ensures an iterative solution.