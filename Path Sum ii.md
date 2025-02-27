# Solution to "113. Path Sum II"

## Problem Statement

Given the root of a binary tree and an integer `targetSum`, return all root-to-leaf paths where the sum of the node values equals `targetSum`.

Each path should be returned as a list of node values.

---

## Approach: Depth-First Search (DFS)

### Explanation

1. Use a recursive DFS approach.
2. At each node, subtract the node value from `targetSum`.
3. If a leaf node is reached and the remaining `targetSum` is zero, record the path.
4. Backtrack to explore other paths.

### Algorithm Steps

1. Perform DFS starting from the root.
2. Maintain a path list to track the current path.
3. If a leaf node is reached with the remaining sum as zero, append the path to the result.
4. Backtrack after exploring left and right subtrees.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def pathSum(self, root: TreeNode, targetSum: int) -> list[list[int]]:
        result = []

        def dfs(node, path, remaining_sum):
            if not node:
                return

            path.append(node.val)
            remaining_sum -= node.val

            if not node.left and not node.right and remaining_sum == 0:
                result.append(list(path))

            dfs(node.left, path, remaining_sum)
            dfs(node.right, path, remaining_sum)

            path.pop()

        dfs(root, [], targetSum)
        return result
```

---

## Example Run

Input:

```python
root = TreeNode(5)
root.left = TreeNode(4)
root.right = TreeNode(8)
root.left.left = TreeNode(11)
root.left.left.left = TreeNode(7)
root.left.left.right = TreeNode(2)
root.right.left = TreeNode(13)
root.right.right = TreeNode(4)
root.right.right.left = TreeNode(5)
root.right.right.right = TreeNode(1)

targetSum = 22
solution = Solution()
print(solution.pathSum(root, targetSum))
```

Output:

```
[[5, 4, 11, 2], [5, 8, 4, 5]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(h)`
    
    - `h` is the height of the tree, due to recursion stack.

---

## Edge Cases

1. Empty tree → Result is `[]`.
2. No valid path → Result is `[]`.
3. Single node equals `targetSum` → Single path returned.

---

## Conclusion

This solution efficiently finds all root-to-leaf paths in a binary tree where the sum equals `targetSum` using a backtracking approach.