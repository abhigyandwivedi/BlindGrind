# 1302. Deepest Leaves Sum

## Problem Statement

Given the `root` of a binary tree, return the sum of values of its deepest leaves.

## Approach

1. Perform a level-order traversal (BFS) to find the deepest level of the tree.
2. Sum the values of all nodes at the deepest level.

## Code Implementation (Python)

### BFS Approach

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def deepestLeavesSum(root: TreeNode) -> int:
    if not root:
        return 0
    
    queue = deque([root])
    
    while queue:
        level_sum = 0
        for _ in range(len(queue)):
            node = queue.popleft()
            level_sum += node.val
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    
    return level_sum
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The queue holds at most one level of nodes, so in the worst case, it stores **O(N)** nodes (for a balanced tree, it's **O(N/2) ≈ O(N)** in the last level).

## Alternative Approach: DFS

Instead of BFS, we can use DFS to keep track of the maximum depth and sum values at that depth.

```python
def deepestLeavesSum_DFS(root: TreeNode) -> int:
    max_depth = 0
    total_sum = 0
    
    def dfs(node, depth):
        nonlocal max_depth, total_sum
        if not node:
            return
        
        if depth > max_depth:
            max_depth = depth
            total_sum = node.val
        elif depth == max_depth:
            total_sum += node.val
        
        dfs(node.left, depth + 1)
        dfs(node.right, depth + 1)
    
    dfs(root, 0)
    return total_sum
```

### Complexity of DFS Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(H)** (recursion stack, where `H` is tree height, worst case **O(N)** for a skewed tree)

## Conclusion

Both BFS and DFS approaches efficiently calculate the sum of the deepest leaves. BFS naturally finds the last level, while DFS explicitly tracks the maximum depth.