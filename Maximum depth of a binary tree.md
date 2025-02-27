# Solution to "104. Maximum Depth of Binary Tree"

## Problem Statement

Given the `root` of a binary tree, return its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Example:

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Recursive Traversal:**
    - If the node is `None`, return `0`.
    - Otherwise, return `1 + max(left_depth, right_depth)`.
2. **Base Case:** An empty tree has a depth of `0`.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def maxDepth(root):
    if not root:
        return 0
    left_depth = maxDepth(root.left)
    right_depth = maxDepth(root.right)
    return 1 + max(left_depth, right_depth)
```

---

## Example Run

Input:

```python
root = TreeNode(3)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)

print(maxDepth(root))
```

Output:

```
3
```

Explanation:

- The longest path is `3 → 20 → 15` or `3 → 20 → 7`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(h)`
    
    - Recursion stack depth equals the height of the tree.

---

## Edge Cases

1. Empty tree → `0`.
2. Single-node tree → `1`.

---

## Conclusion

Using recursion efficiently calculates the maximum depth of a binary tree.