# 2331. Evaluate Boolean Binary Tree

## Problem Statement

Given the `root` of a full binary tree where each node contains a value:

- `0` represents `False`
- `1` represents `True`
- `2` represents logical OR (`||`)
- `3` represents logical AND (`&&`)

Evaluate the boolean value of the tree.

## Approach

We can solve this problem using a recursive Depth-First Search (DFS):

1. If the node is a leaf (`0` or `1`), return its boolean value.
2. If the node is an OR (`2`), return the logical OR of its left and right children.
3. If the node is an AND (`3`), return the logical AND of its left and right children.
4. Recursively evaluate the left and right subtrees.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def evaluateTree(root: TreeNode) -> bool:
    if root.val == 0:
        return False
    if root.val == 1:
        return True
    
    left_val = evaluateTree(root.left)
    right_val = evaluateTree(root.right)
    
    if root.val == 2:  # OR operation
        return left_val or right_val
    if root.val == 3:  # AND operation
        return left_val and right_val
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.

## Conclusion

This approach efficiently evaluates the boolean value of a full binary tree using recursion. The recursive DFS traversal ensures an optimal time complexity of **O(N)**.