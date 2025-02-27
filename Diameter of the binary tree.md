# Solution to "543. Diameter of Binary Tree"

## Problem Statement

Given the root of a binary tree, return the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:

```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: The longest path is [4, 2, 1, 3] or [5, 2, 1, 3], with length 3.
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Recursive DFS:** For each node, calculate the height of the left and right subtrees.
2. **Diameter Calculation:** The diameter at each node is the sum of the heights of its left and right subtrees.
3. **Update Maximum:** Keep track of the maximum diameter found during traversal.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def diameterOfBinaryTree(root: TreeNode) -> int:
    diameter = 0

    def depth(node):
        nonlocal diameter
        if not node:
            return 0
        left = depth(node.left)
        right = depth(node.right)
        diameter = max(diameter, left + right)
        return 1 + max(left, right)

    depth(root)
    return diameter
```

---

## Example Run

Input:

```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
root.left.right = TreeNode(5)

print(diameterOfBinaryTree(root))
```

Output:

```
3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(H)`
    
    - `H` is the height of the tree due to recursion stack.

---

## Edge Cases

1. Single node → Diameter is 0.
2. Linear tree → Diameter equals the number of edges.

---

## Conclusion

This DFS-based approach efficiently calculates the diameter of a binary tree by recursively determining the height of each subtree.