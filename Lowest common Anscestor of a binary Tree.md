# Solution to "236. Lowest Common Ancestor of a Binary Tree"

## Problem Statement

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes `p` and `q`.

According to the definition of LCA: “The lowest common ancestor of two nodes `p` and `q` is the lowest node in the tree that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).”

Example:

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3

Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
```

---

## Approach: Recursive DFS

### Explanation

1. **Base Case:** If the current node is null, `p`, or `q`, return the current node.
2. **Recursive Search:** Search both left and right subtrees.
3. **Result:** If both left and right return non-null values, the current node is the LCA. Otherwise, return the non-null value.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        if not root or root == p or root == q:
            return root

        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        if left and right:
            return root
        return left if left else right
```

---

## Example Run

Input:

```python
root = TreeNode(3)
root.left = TreeNode(5)
root.right = TreeNode(1)
root.left.left = TreeNode(6)
root.left.right = TreeNode(2)
root.right.left = TreeNode(0)
root.right.right = TreeNode(8)
root.left.right.left = TreeNode(7)
root.left.right.right = TreeNode(4)
p = root.left
q = root.right

solution = Solution()
result = solution.lowestCommonAncestor(root, p, q)
print(result.val)  # Output: 3
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
    
    - Recursion stack space, where `H` is the height of the tree.

---

## Edge Cases

1. If one node is the ancestor of the other, the ancestor is the LCA.
2. If either `p` or `q` is the root, the root is the LCA.

---

## Conclusion

This solution efficiently finds the LCA using recursive depth-first search, ensuring correctness in all cases.