# Solution to "105. Construct Binary Tree from Preorder and Inorder Traversal"

## Problem Statement

Given two integer arrays `preorder` and `inorder` where:

- `preorder` is the preorder traversal of a binary tree,
- `inorder` is the inorder traversal of the same tree, construct and return the binary tree.

Example:

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

---

## Approach: Recursive Tree Construction

### Explanation

1. **Preorder Insight:** The first element of `preorder` is always the root.
2. **Inorder Insight:** Find the root in `inorder` to divide into left and right subtrees.
3. **Recursion:** Recursively build left and right subtrees using corresponding `preorder` and `inorder` segments.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def buildTree(preorder, inorder):
    if not preorder or not inorder:
        return None

    # Root is the first element in preorder
    root_val = preorder[0]
    root = TreeNode(root_val)

    # Find root index in inorder
    root_index = inorder.index(root_val)

    # Recursively build left and right subtrees
    root.left = buildTree(preorder[1:1 + root_index], inorder[:root_index])
    root.right = buildTree(preorder[1 + root_index:], inorder[root_index + 1:])

    return root
```

---

## Example Run

Input:

```python
preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
root = buildTree(preorder, inorder)
```

Output:

```
Tree structure: [3,9,20,null,null,15,7]
```

Explanation:

- The root is `3` (first in preorder).
- Left subtree from `inorder[:1]` and `preorder[1:2]` → `9`.
- Right subtree from `inorder[2:]` and `preorder[2:]` → `20` with children `15` and `7`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is processed once using index lookup.
2. **Space Complexity:** `O(n)`
    
    - Recursion stack depth can reach `n` in the worst case (skewed tree).

---

## Edge Cases

1. If `preorder` or `inorder` is empty, return `None`.
2. Single node input returns a single-node tree.

---

## Conclusion

This recursive approach efficiently reconstructs the binary tree using preorder and inorder traversals.