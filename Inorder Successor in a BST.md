# Solution to "285. Inorder Successor in BST"

## Problem Statement

Given the `root` of a binary search tree (BST) and a node `p`, find the inorder successor of node `p` in the BST.

The inorder successor of a node `p` is the node with the smallest key greater than `p.val`. If no such node exists, return `None`.

---

## Approach: BST Traversal

### Explanation

We leverage the properties of a BST to find the inorder successor efficiently.

### Algorithm Steps

1. **Case 1: Right Subtree Exists:**
    
    - If `p` has a right child, the successor is the leftmost node of the right subtree.
2. **Case 2: No Right Subtree:**
    
    - If no right child exists, traverse from the root, updating the successor whenever we move left.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderSuccessor(self, root: TreeNode, p: TreeNode) -> TreeNode:
        successor = None
        while root:
            if p.val < root.val:
                successor = root
                root = root.left
            else:
                root = root.right
        return successor
```

---

## Example Run

Input:

```python
root = TreeNode(5)
root.left = TreeNode(3)
root.right = TreeNode(8)
root.left.left = TreeNode(2)
root.left.right = TreeNode(4)
p = root.left  # Node with value 3

solution = Solution()
successor = solution.inorderSuccessor(root, p)
print(successor.val if successor else None)
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(h)`
    
    - `h` is the height of the BST. In the worst case, it is `O(n)` for a skewed tree and `O(log n)` for a balanced tree.
2. **Space Complexity:** `O(1)`
    
    - Only a few variables are used.

---

## Edge Cases

1. No successor → Output: `None`.
2. Successor is the root → Properly identified.

---

## Conclusion

This solution efficiently finds the inorder successor by leveraging the BST's structure, achieving optimal time complexity.