# Solution to "226. Invert Binary Tree"

## Problem Statement

Given the root of a binary tree, invert the tree and return its root.

Example:

```
Input:
    4
   / \
  2   7
 / \ / \
1  3 6  9

Output:
    4
   / \
  7   2
 / \ / \
9  6 3  1
```

---

## Approach: Recursive Depth-First Search (DFS)

### Explanation

1. **Recursive Swap:**
    - Swap the left and right child of each node recursively.
    - If the node is `None`, return `None`.
2. **Base Case:**
    - If the node is `None`, return `None`.
3. **Recursive Case:**
    - Swap the left and right subtrees.

---

## Implementation in Python

```python
def invertTree(root):
    if not root:
        return None

    # Swap left and right children
    root.left, root.right = invertTree(root.right), invertTree(root.left)

    return root

# Example usage
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Create example tree
root = TreeNode(4)
root.left = TreeNode(2, TreeNode(1), TreeNode(3))
root.right = TreeNode(7, TreeNode(6), TreeNode(9))

# Invert tree
inverted_root = invertTree(root)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - Each node is visited once.
2. **Space Complexity:** `O(h)` - Height of the recursion stack, where `h` is the tree height.

---

## Example Run

Input:

```
    4
   / \
  2   7
 / \ / \
1  3 6  9
```

Output:

```
    4
   / \
  7   2
 / \ / \
9  6 3  1
```

---

## Edge Cases

1. Empty tree returns `None`.
2. Single node tree returns the same node.

---

## Conclusion

This solution efficiently inverts a binary tree using a recursive approach, ensuring each node's children are swapped.