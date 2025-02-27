# Solution to "199. Binary Tree Right Side View"

## Problem Statement

Given the `root` of a binary tree, imagine yourself standing on the right side of it. Return the values of the nodes you can see ordered from top to bottom.

Example:

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

---

## Approach: Level-Order Traversal (BFS)

### Explanation

1. **Use a Queue:** Perform level-order traversal using a queue.
2. **Track Rightmost Node:** For each level, store the last node encountered.

---

## Implementation in Python

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def rightSideView(root: TreeNode) -> list[int]:
    if not root:
        return []

    queue = deque([root])
    result = []

    while queue:
        level_size = len(queue)
        for i in range(level_size):
            node = queue.popleft()
            if i == level_size - 1:
                result.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return result
```

---

## Example Run

Input:

```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.right = TreeNode(5)
root.right.right = TreeNode(4)

print(rightSideView(root))
```

Output:

```
[1, 3, 4]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is processed once.
2. **Space Complexity:** `O(n)`
    
    - Queue stores nodes level by level.

---

## Edge Cases

1. Empty tree → Return `[]`.
2. Single node → Return `[root.val]`.
3. Balanced and unbalanced trees → Properly handled.

---

## Conclusion

Using BFS ensures an efficient solution to capture the rightmost view of a binary tree in linear time.