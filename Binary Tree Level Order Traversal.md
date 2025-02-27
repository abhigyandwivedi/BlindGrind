# Solution to "102. Binary Tree Level Order Traversal"

## Problem Statement

Given the root of a binary tree, return the level order traversal of its nodes' values (i.e., from left to right, level by level).

Example:

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

---

## Approach: Breadth-First Search (BFS)

### Explanation

1. **Use a Queue:** Start with the root node and traverse level by level using a queue.
2. **Process Each Level:** For each level, collect all node values and add their children to the queue.
3. **Store Results:** Append the values of each level to the final result list.

---

## Implementation in Python

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def levelOrder(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)

    return result

# Example usage
# root = TreeNode(3)
# root.left = TreeNode(9)
# root.right = TreeNode(20, TreeNode(15), TreeNode(7))
# print(levelOrder(root))  # Output: [[3], [9, 20], [15, 7]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` where `n` is the number of nodes in the tree. Each node is processed once.
2. **Space Complexity:** `O(n)` for storing the nodes in the queue and the result list.

---

## Example Run

Input:

```
[3,9,20,null,null,15,7]
```

Output:

```
[[3], [9, 20], [15, 7]]
```

---

## Edge Cases

1. Empty tree: `None` → Output: `[]`
2. Single node: `[1]` → Output: `[[1]]`
3. Only left children: `[1,2,null,3]` → Output: `[[1], [2], [3]]`

---

## Conclusion

This solution efficiently performs a level order traversal of a binary tree using a queue, ensuring linear time complexity.