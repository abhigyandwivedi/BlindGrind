# Solution to "124. Binary Tree Maximum Path Sum"

## Problem Statement

Given the root of a binary tree, return the maximum path sum. A path in a binary tree is a sequence of nodes where each pair of adjacent nodes has an edge connecting them. A node can only appear once in the path, and the path does not necessarily pass through the root.

---

## Approach: Depth-First Search (DFS)

### Explanation

We use a recursive DFS approach:

1. For each node, calculate the maximum path sum passing through that node.
2. The path can either:
    - Continue through the left or right subtree.
    - End at the current node.
    - Form a new path passing through the current node and both subtrees.
3. Track the global maximum path sum.

### Algorithm Steps

1. Perform a DFS traversal.
2. For each node, calculate:
    - `leftMax`: Maximum path sum from the left subtree.
    - `rightMax`: Maximum path sum from the right subtree.
    - `currentMax`: Path sum including the current node and both subtrees.
3. Update the global maximum if `currentMax` is greater.
4. Return the maximum path sum ending at the current node (`node.val + max(leftMax, rightMax)`).

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        self.maxSum = float('-inf')

        def dfs(node):
            if not node:
                return 0

            leftMax = max(dfs(node.left), 0)
            rightMax = max(dfs(node.right), 0)

            currentMax = node.val + leftMax + rightMax
            self.maxSum = max(self.maxSum, currentMax)

            return node.val + max(leftMax, rightMax)

        dfs(root)
        return self.maxSum
```

---

## Example Run

Input:

```python
root = TreeNode(-10)
root.left = TreeNode(9)
root.right = TreeNode(20)
root.right.left = TreeNode(15)
root.right.right = TreeNode(7)

solution = Solution()
print(solution.maxPathSum(root))
```

Output:

```
42
```

Explanation: The optimal path is `15 → 20 → 7` with a sum of `42`.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(h)`
    
    - Recursive stack space, where `h` is the height of the tree.

---

## Edge Cases

1. Single node → Output is the node's value.
2. All negative values → Choose the least negative node.

---

## Conclusion

This solution efficiently computes the maximum path sum using a depth-first search approach, ensuring linear time complexity.