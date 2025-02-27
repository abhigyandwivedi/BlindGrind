# Solution to "98. Validate Binary Search Tree"

## Problem Statement

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

1. The left subtree of a node contains only nodes with keys **less than** the node's key.
2. The right subtree of a node contains only nodes with keys **greater than** the node's key.
3. Both the left and right subtrees must also be binary search trees.

Example:

```
Input: root = [2,1,3]
Output: true

Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but the right child's value is 4, violating the BST rule.
```

---

## Approach: Inorder Traversal with Range Validation

### Explanation

1. **Recursive Range Check:** For each node, ensure its value lies within a valid range determined by its parent nodes.
2. **Inorder Traversal:** A valid BST's inorder traversal produces values in strictly increasing order.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def isValidBST(root):
    def validate(node, low=float('-inf'), high=float('inf')):
        if not node:
            return True
        if not (low < node.val < high):
            return False
        return (validate(node.left, low, node.val) and
                validate(node.right, node.val, high))

    return validate(root)

# Example usage
root = TreeNode(2)
root.left = TreeNode(1)
root.right = TreeNode(3)
print(isValidBST(root))  # Output: True
```

---

## Example Run

Input:

```python
root = TreeNode(5)
root.left = TreeNode(1)
root.right = TreeNode(4)
root.right.left = TreeNode(3)
root.right.right = TreeNode(6)
print(isValidBST(root))
```

Output:

```
False
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(h)`
    
    - `h` is the height of the tree, due to the recursion stack.

---

## Edge Cases

1. Empty tree: Return `True` (an empty tree is a valid BST).
2. Single node: Return `True`.
3. Invalid BST due to child values: Ensure range checks are applied correctly.

---

## Conclusion

This solution efficiently validates a binary search tree using recursive range checks, ensuring correctness across all edge cases.