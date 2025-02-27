# Second Minimum Node in a Binary Tree

## Problem Statement

Given a non-empty special binary tree consisting of nodes with unique values:

- The root node has the smallest value.
- Every node has at most two children.
- Each node's value is either equal to its parent or greater.

Find the second minimum value in the tree. If there is no second minimum, return `-1`.

## Approach

1. Perform a traversal of the tree to identify the second minimum value.
2. The smallest value is at the root. We need to find the smallest value that is greater than the root value.
3. If a node’s value is greater than the root, we track it as a potential second minimum.
4. Use DFS or BFS to explore all nodes.

## Code Implementation (Python)

### Recursive Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def findSecondMinimumValue(root: TreeNode) -> int:
    second_min = float('inf')
    min_val = root.val
    
    def traverse(node):
        nonlocal second_min
        if not node:
            return
        if min_val < node.val < second_min:
            second_min = node.val
        elif node.val == min_val:
            traverse(node.left)
            traverse(node.right)
    
    traverse(root)
    return second_min if second_min != float('inf') else -1
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.

## Alternative Approach: Iterative Using BFS

Instead of recursion, we can use a queue to traverse the tree iteratively:

```python
from collections import deque

def findSecondMinimumValue_iterative(root: TreeNode) -> int:
    min_val = root.val
    second_min = float('inf')
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        if min_val < node.val < second_min:
            second_min = node.val
        elif node.val == min_val:
            if node.left:
                queue.append(node.left)
                queue.append(node.right)
    
    return second_min if second_min != float('inf') else -1
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(N)** (queue holds nodes in worst case)

## Conclusion

Both recursive and iterative approaches efficiently find the second minimum node in a binary tree. The iterative BFS method avoids recursion depth issues, while the recursive approach is more intuitive.