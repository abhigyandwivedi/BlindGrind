# 1469. Find All The Lonely Nodes

## Problem Statement

Given the `root` of a binary tree, return an array containing the values of all **lonely** nodes in the tree. A lonely node is a node that has only one child.

## Approach

We can solve this problem using a Depth-First Search (DFS) or Breadth-First Search (BFS) traversal:

1. Traverse the tree using DFS or BFS.
2. If a node has only one child (either left or right), add that child to the result list.
3. Continue traversing until all nodes have been checked.

## Code Implementation (Python)

### DFS Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def findLonelyNodes(root: TreeNode) -> list[int]:
    lonely_nodes = []
    
    def dfs(node: TreeNode):
        if not node:
            return
        
        if node.left and not node.right:
            lonely_nodes.append(node.left.val)
        elif node.right and not node.left:
            lonely_nodes.append(node.right.val)
        
        dfs(node.left)
        dfs(node.right)
    
    dfs(root)
    return lonely_nodes
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The space complexity is **O(H)**, where `H` is the height of the tree due to recursion.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.

## Alternative Approach: BFS

Instead of recursion, we can use a queue to implement an iterative BFS approach.

```python
from collections import deque

def findLonelyNodes_bfs(root: TreeNode) -> list[int]:
    lonely_nodes = []
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        
        if node.left and not node.right:
            lonely_nodes.append(node.left.val)
        elif node.right and not node.left:
            lonely_nodes.append(node.right.val)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    
    return lonely_nodes
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is visited once)
- **Space Complexity**: **O(N)** (queue can store up to `N` nodes in the worst case)

## Conclusion

Both DFS and BFS solutions efficiently find all lonely nodes in a binary tree. The recursive DFS approach is concise, while the iterative BFS approach avoids function call overhead.