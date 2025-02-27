# Solution to "662. Maximum Width of Binary Tree"

## Problem Statement

Given the `root` of a binary tree, return the **maximum width** of the tree. The width of a level is defined as the number of nodes between the leftmost and rightmost non-null nodes in that level.

---

## Approach: Level-Order Traversal with Indexing

### Explanation

1. Perform a level-order traversal using a queue.
2. Store each node along with its index, similar to a binary heap index.
3. At each level, calculate the width as `rightmost_index - leftmost_index + 1`.
4. Track the maximum width across all levels.

### Algorithm Steps

1. **Queue Initialization:** Start with the root node and index `0`.
2. **Level Traversal:** For each level:
    - Record the first and last indices.
    - Add children with updated indices (`2 * index` for left, `2 * index + 1` for right).
3. **Width Calculation:** Calculate the width for each level and update the maximum.

---

## Implementation in Python

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def widthOfBinaryTree(self, root: TreeNode) -> int:
        if not root:
            return 0

        queue = deque([(root, 0)])
        max_width = 0

        while queue:
            level_length = len(queue)
            _, first_index = queue[0]

            for _ in range(level_length):
                node, index = queue.popleft()

                if node.left:
                    queue.append((node.left, 2 * index))
                if node.right:
                    queue.append((node.right, 2 * index + 1))

            _, last_index = queue[-1] if queue else (None, first_index)
            max_width = max(max_width, last_index - first_index + 1)

        return max_width
```

---

## Example Run

Input:

```python
root = TreeNode(1)
root.left = TreeNode(3)
root.right = TreeNode(2)
root.left.left = TreeNode(5)
root.left.right = TreeNode(3)
root.right.right = TreeNode(9)

solution = Solution()
print(solution.widthOfBinaryTree(root))
```

Output:

```
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is processed once during level-order traversal.
2. **Space Complexity:** `O(n)`
    
    - Queue stores nodes at each level, with the maximum being the width of the last level.

---

## Edge Cases

1. Single node → Width is `1`.
2. Empty tree → Width is `0`.
3. Unbalanced tree → Width is determined by the widest level.

---

## Conclusion

This solution efficiently calculates the maximum width of a binary tree using a level-order traversal approach with indexing.