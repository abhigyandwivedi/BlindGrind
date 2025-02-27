# Solution to "110. Balanced Binary Tree"

## Problem Statement

Given a binary tree, determine if it is height-balanced. A binary tree is balanced if the depth of the two subtrees of every node never differs by more than one.

Example:

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

---

## Approach: Recursive Depth-First Search (DFS)

### Explanation

1. **Height Calculation:** Recursively calculate the height of left and right subtrees.
2. **Balance Check:** If the height difference between left and right subtrees is greater than 1, the tree is unbalanced.
3. **Return:** If all nodes satisfy the condition, the tree is balanced.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def isBalanced(root: TreeNode) -> bool:
    def height(node):
        if not node:
            return 0
        left_height = height(node.left)
        right_height = height(node.right)
        if left_height == -1 or right_height == -1 or abs(left_height - right_height) > 1:
            return -1
        return 1 + max(left_height, right_height)

    return height(root) != -1

# Example usage
# root = TreeNode(3)
# root.left = TreeNode(9)
# root.right = TreeNode(20, TreeNode(15), TreeNode(7))
# print(isBalanced(root))  # Output: True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - Each node is visited once.
2. **Space Complexity:** `O(h)` - Recursive stack space, where `h` is the height of the tree.

---

## Example Run

Input:

```
root = [3,9,20,null,null,15,7]
```

Output:

```
True
```

---

## Edge Cases

1. Empty tree → `True`
2. Single node → `True`
3. Unbalanced subtree → `False`

---

## Conclusion

This solution efficiently determines if a binary tree is height-balanced using recursive DFS, ensuring linear time complexity and logarithmic space complexity.