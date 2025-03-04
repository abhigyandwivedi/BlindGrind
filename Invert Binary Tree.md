#DFS #dfs
# Solution to "226. Invert Binary Tree"

## Problem Statement

Given the root of a binary tree, invert the tree and return its root.

Example:

```
Input:
    4
   / \
  2   7
 / \ / \
1  3 6  9

Output:
    4
   / \
  7   2
 / \ / \
9  6 3  1
```

---

## Approach: Recursive Depth-First Search (DFS)

### Explanation

1. **Recursive Swap:**
    - Swap the left and right child of each node recursively.
    - If the node is `None`, return `None`.
2. **Base Case:**
    - If the node is `None`, return `None`.
3. **Recursive Case:**
    - Swap the left and right subtrees.

---

## Implementation in Python

```python
def invertTree(root):
    if not root:
        return None

    # Swap left and right children
    root.left, root.right = invertTree(root.right), invertTree(root.left)

    return root

# Example usage
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Create example tree
root = TreeNode(4)
root.left = TreeNode(2, TreeNode(1), TreeNode(3))
root.right = TreeNode(7, TreeNode(6), TreeNode(9))

# Invert tree
inverted_root = invertTree(root)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - Each node is visited once.
2. **Space Complexity:** `O(h)` - Height of the recursion stack, where `h` is the tree height.

---

## Example Run

Input:

```
    4
   / \
  2   7
 / \ / \
1  3 6  9
```

Output:

```
    4
   / \
  7   2
 / \ / \
9  6 3  1
```

---

## Edge Cases

1. Empty tree returns `None`.
2. Single node tree returns the same node.

---

## Conclusion

This solution efficiently inverts a binary tree using a recursive approach, ensuring each node's children are swapped.

# Reverse Odd Levels of Binary Tree (LeetCode 2415)
https://leetcode.com/problems/reverse-odd-levels-of-binary-tree/ 
#bfs #BFS

## Problem Statement

Given the `root` of a **perfect binary tree**, reverse the values of the nodes at each **odd level** of the tree.

- A **perfect binary tree** is a binary tree where all levels are completely filled.
- The **root** is at level **0**.
- Swap the values at odd levels but do not change the tree structure.

### Example 1:

#### Input:

```plaintext
        2
       / \
      3   5
     / \ / \
    8 13 21 34
```

#### Output:

```plaintext
        2
       / \
      5   3
     / \ / \
    8 13 21 34
```

#### Explanation:

- Level **0**: `[2]` (unchanged)
- Level **1**: `[3, 5]` → Reverse → `[5, 3]`
- Level **2**: `[8, 13, 21, 34]` (unchanged)

---

### Example 2:

#### Input:

```plaintext
        7
       / \
      13  11
     / \   / \
    1   9 15  5
```

#### Output:

```plaintext
        7
       / \
      11  13
     / \   / \
    1   9 15  5
```

---

## Solution Explanation

### Approach: BFS (Level Order Traversal)

Since we need to reverse values **only at odd levels**, we perform a level order traversal and process odd levels separately.

### Algorithm Steps:

1. **Perform Level Order Traversal**: Use a queue to traverse the tree level by level.
2. **Identify Odd Levels**: Track the current level index and reverse values at odd levels.
3. **Swap Values In-Place**: Instead of modifying node connections, only swap node values.

---

## Code Implementation (Python)

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def reverseOddLevels(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        
        queue = deque([root])
        level = 0
        
        while queue:
            level_size = len(queue)
            nodes = []
            
            for _ in range(level_size):
                node = queue.popleft()
                nodes.append(node)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
            if level % 2 == 1:
                left, right = 0, len(nodes) - 1
                while left < right:
                    nodes[left].val, nodes[right].val = nodes[right].val, nodes[left].val
                    left += 1
                    right -= 1
            
            level += 1
        
        return root
```

---

## Complexity Analysis

- **Time Complexity**: `O(n)` (Each node is processed once)
- **Space Complexity**: `O(n)` (For storing nodes in the queue)

---

## Summary

- We **traverse the tree level by level** using BFS.
- **Reverse only the odd levels** without modifying tree structure.
- Efficient `O(n)` solution using **deque** for level-order traversal.

This method ensures that the tree remains perfect while reversing values only at odd levels. 🚀