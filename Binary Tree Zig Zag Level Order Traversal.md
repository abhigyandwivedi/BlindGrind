# Solution to "103. Binary Tree Zigzag Level Order Traversal"

## Problem Statement

Given the `root` of a binary tree, return the zigzag level order traversal of its nodes' values.

- In zigzag traversal:
    - The first level is traversed from left to right.
    - The second level is traversed from right to left.
    - The third level is traversed from left to right, and so on.

---

## Approach: Breadth-First Search (BFS) with Queue

### Explanation

We can use a **Breadth-First Search (BFS)** approach to traverse the tree level by level. To achieve the zigzag pattern:

1. **Use a Queue:**
    
    - Enqueue the root node and process nodes level by level.
2. **Direction Toggle:**
    
    - Use a boolean flag `left_to_right` to determine the order.
3. **Level Processing:**
    
    - For each level:
        - Collect node values.
        - If `left_to_right` is `True`, append values normally.
        - If `False`, reverse the values before adding them to the result.
4. **Toggle the Direction:**
    
    - After processing each level, flip the `left_to_right` flag.

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
    def zigzagLevelOrder(self, root: TreeNode):
        if not root:
            return []

        result = []
        queue = deque([root])
        left_to_right = True

        while queue:
            level_size = len(queue)
            current_level = []

            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            # Reverse if the direction is right to left
            if not left_to_right:
                current_level.reverse()

            result.append(current_level)
            left_to_right = not left_to_right

        return result
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

solution = Solution()
print(solution.zigzagLevelOrder(root))
```

Output:

```
[[3], [20, 9], [15, 7]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - We visit each node once, where `N` is the number of nodes in the tree.
2. **Space Complexity:** `O(N)`
    
    - The queue holds nodes level by level, and the result stores all node values.

---

## Edge Cases

1. If the tree is empty (`root = None`), return `[]`.
2. If the tree has only one node, return `[[root.val]]`.
3. Handles imbalanced trees and nodes with `None` children.

---

## Conclusion

Using BFS with a queue and toggling the traversal direction ensures an efficient solution for zigzag level order traversal of a binary tree.