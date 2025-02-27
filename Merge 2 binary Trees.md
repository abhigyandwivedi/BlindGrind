# 617. Merge Two Binary Trees

## Problem Statement

Given two binary trees, `root1` and `root2`, merge them into a single binary tree. The merging rules are:

1. If two nodes overlap, sum their values as the new value.
2. If one node is `None`, use the non-null node as part of the new tree.
3. The merging process continues recursively for left and right children.

## Approach

We can solve this problem using a Depth-First Search (DFS) approach:

1. If both nodes are `None`, return `None`.
2. If only one node is `None`, return the non-null node.
3. Otherwise, create a new node with the sum of both nodes' values.
4. Recursively merge the left and right subtrees.

## Code Implementation (Python)

### Recursive DFS Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def mergeTrees(root1: TreeNode, root2: TreeNode) -> TreeNode:
    if not root1:
        return root2
    if not root2:
        return root1
    
    merged_root = TreeNode(root1.val + root2.val)
    merged_root.left = mergeTrees(root1.left, root2.left)
    merged_root.right = mergeTrees(root1.right, root2.right)
    
    return merged_root
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the minimum number of nodes in `root1` and `root2`.

## Space Complexity Analysis

- The space complexity is **O(H)**, where `H` is the height of the tree due to recursion.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.

## Alternative Approach: Iterative BFS

Instead of recursion, we can use a queue to implement an iterative BFS approach.

```python
from collections import deque

def mergeTrees_iterative(root1: TreeNode, root2: TreeNode) -> TreeNode:
    if not root1:
        return root2
    if not root2:
        return root1
    
    queue = deque([(root1, root2)])
    
    while queue:
        node1, node2 = queue.popleft()
        node1.val += node2.val
        
        if node1.left and node2.left:
            queue.append((node1.left, node2.left))
        elif not node1.left:
            node1.left = node2.left
        
        if node1.right and node2.right:
            queue.append((node1.right, node2.right))
        elif not node1.right:
            node1.right = node2.right
    
    return root1
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is visited once)
- **Space Complexity**: **O(N)** (queue can store up to `N` nodes in the worst case)

## Conclusion

Both DFS and BFS solutions efficiently merge two binary trees. The recursive DFS approach is straightforward, while the iterative BFS approach avoids recursion overhead.