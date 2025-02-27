# Solution to "235. Lowest Common Ancestor of a Binary Search Tree"

## Problem Statement

Given a Binary Search Tree (BST), find the lowest common ancestor (LCA) of two given nodes `p` and `q`.

Example:

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
```

---

## Approach: Recursive BST Traversal

### Explanation

1. **Binary Search Property:** In a BST, the left subtree contains values less than the root, and the right subtree contains values greater than the root.
2. **Traversal:**
    - If both `p` and `q` are smaller than the root, search in the left subtree.
    - If both are greater, search in the right subtree.
    - Otherwise, the current node is the LCA.

---

## Implementation in Python

```python
def lowestCommonAncestor(root, p, q):
    if not root:
        return None

    # If both nodes are smaller, go left
    if p.val < root.val and q.val < root.val:
        return lowestCommonAncestor(root.left, p, q)

    # If both nodes are greater, go right
    if p.val > root.val and q.val > root.val:
        return lowestCommonAncestor(root.right, p, q)

    # Otherwise, root is the LCA
    return root

# Example usage
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Example BST
root = TreeNode(6)
root.left = TreeNode(2)
root.right = TreeNode(8)
root.left.left = TreeNode(0)
root.left.right = TreeNode(4)
root.right.left = TreeNode(7)
root.right.right = TreeNode(9)
root.left.right.left = TreeNode(3)
root.left.right.right = TreeNode(5)

p = root.left  # Node 2
q = root.right  # Node 8

result = lowestCommonAncestor(root, p, q)
print(result.val)  # Output: 6
```

---

## Complexity Analysis

1. **Time Complexity:** `O(h)` - `h` is the height of the tree, as we traverse down the tree based on the BST property.
2. **Space Complexity:** `O(h)` - Due to the recursive call stack.

---

## Example Run

Input:

```
root = [6,2,8,0,4,7,9,null,null,3,5]
p = 2, q = 8
```

Output:

```
6
```

---

## Edge Cases

1. One node is the ancestor of the other → Ancestor node is the LCA.
2. Both nodes on opposite sides → Root becomes LCA.

---

## Conclusion

This solution efficiently finds the LCA using BST properties, ensuring optimal traversal.