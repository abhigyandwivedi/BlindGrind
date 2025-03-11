# 776. Split BST

## Problem Statement

Given the root of a Binary Search Tree (BST) and an integer `target`, split the tree into two subtrees:

1. One subtree containing all nodes with values **≤ target**.
2. Another subtree containing all nodes with values **> target**.

Return the roots of the two subtrees as a list `[left_subtree, right_subtree]`.

## Approach

1. Use a recursive function to traverse the tree.
2. If `root.val` is **≤ target**, the root belongs to the left subtree:
    - Recursively split the right subtree.
    - Attach the left result of the split to `root.right`.
3. If `root.val` is **> target**, the root belongs to the right subtree:
    - Recursively split the left subtree.
    - Attach the right result of the split to `root.left`.
4. Return the two resulting subtrees.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def splitBST(root: TreeNode, target: int):
    if not root:
        return [None, None]
    
    if root.val <= target:
        left_subtree, right_subtree = self.splitBST(root.right, target)
        root.right = left_subtree
        return [root, right_subtree]
    else:
        left_subtree, right_subtree = self.splitBST(root.left, target)
        root.left = right_subtree
        return [left_subtree, root]
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.
- In a balanced BST, traversal is limited to **O(log N)** nodes, making the average case **O(log N)**.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In the worst case (skewed tree), **O(N)** space is required.
- In a balanced tree, **O(log N)** space is used.

## Conclusion

This approach efficiently splits a BST while preserving its structure. The algorithm runs in **O(H)** time and space, making it optimal for large BSTs.