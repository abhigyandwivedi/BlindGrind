# 2236. Root Equals Sum of Children

## Problem Statement

Given a binary tree where the root node has exactly two children, determine if the value of the root is equal to the sum of the values of its two children.

## Approach

Since the root has exactly two children, we can solve this problem with a simple conditional check:

1. If the root is `None`, return `False` (invalid case).
2. Check if the root's value is equal to the sum of its left and right child values.
3. Return `True` if the condition holds, otherwise return `False`.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def checkTree(root: TreeNode) -> bool:
    return root.val == root.left.val + root.right.val
```

## Time Complexity Analysis

- The function performs a constant number of operations, leading to **O(1)** complexity.

## Space Complexity Analysis

- The function does not use any extra space apart from input parameters, leading to **O(1)** space complexity.

## Conclusion

This is a simple problem that can be solved in constant time and space using a straightforward comparison.