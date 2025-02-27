# 1379. Find a Corresponding Node of a Binary Tree in a Clone of That Tree

## Problem Statement

Given two binary trees, `original` and `cloned`, and a reference to a target node in the `original` tree, find the corresponding node in the `cloned` tree.

## Approach

Since the `cloned` tree is an exact copy of the `original` tree, the structure and node values remain the same. A depth-first search (DFS) or breadth-first search (BFS) can be used to find the corresponding node in the `cloned` tree.

### DFS Approach (Recursive)

1. If the current node in `original` is `None`, return `None`.
2. If the current node in `original` is the target node, return the corresponding node in `cloned`.
3. Recursively search in the left and right subtrees.
4. Return the corresponding node if found.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def getTargetCopy(original: TreeNode, cloned: TreeNode, target: TreeNode) -> TreeNode:
    if not original:
        return None
    
    if original is target:
        return cloned
    
    left_result = getTargetCopy(original.left, cloned.left, target)
    if left_result:
        return left_result
    
    return getTargetCopy(original.right, cloned.right, target)
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The space complexity is **O(H)**, where `H` is the height of the tree.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.

## Alternative Approach: Iterative BFS

Instead of recursion, we can use a queue to implement an iterative BFS approach.

```python
from collections import deque

def getTargetCopy_iterative(original: TreeNode, cloned: TreeNode, target: TreeNode) -> TreeNode:
    queue = deque([(original, cloned)])
    
    while queue:
        orig_node, clone_node = queue.popleft()
        
        if orig_node is target:
            return clone_node
        
        if orig_node.left:
            queue.append((orig_node.left, clone_node.left))
        if orig_node.right:
            queue.append((orig_node.right, clone_node.right))
    
    return None
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is visited once)
- **Space Complexity**: **O(N)** (queue can store up to `N` nodes in the worst case)

## Conclusion

Both recursive DFS and iterative BFS solutions efficiently find the corresponding node in the cloned tree. The recursive approach is concise, while the iterative approach avoids function call overhead.