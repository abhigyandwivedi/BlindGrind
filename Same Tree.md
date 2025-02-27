# Solution to "100. Same Tree"

## Problem Statement

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

---

## Approach: Recursive Depth-First Search (DFS)

### Explanation

We traverse both trees simultaneously and compare each corresponding node.

### Algorithm Steps

1. **Base Case:** If both nodes are `None`, return `True`.
2. **Mismatch:** If one is `None` and the other is not, or if values differ, return `False`.
3. **Recursive Check:** Recursively check the left and right subtrees.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if not p or not q or p.val != q.val:
            return False
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```

---

## Example Run

Input:

```python
p = TreeNode(1)
p.left = TreeNode(2)
p.right = TreeNode(3)

q = TreeNode(1)
q.left = TreeNode(2)
q.right = TreeNode(3)

solution = Solution()
print(solution.isSameTree(p, q))
```

Output:

```
True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - `n` is the number of nodes. Each node is visited once.
2. **Space Complexity:** `O(h)`
    
    - `h` is the height of the tree, due to recursion stack.

---

## Edge Cases

1. Both trees empty → Output: `True`.
2. One tree empty, one non-empty → Output: `False`.
3. Same structure but different values → Output: `False`.

---

## Conclusion

This solution efficiently checks whether two binary trees are identical by recursively comparing each node.