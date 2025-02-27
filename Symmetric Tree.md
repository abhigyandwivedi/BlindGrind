# LeetCode 101: Symmetric Tree

## Problem Statement

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

### Example Input

```
Input: root = [1,2,2,3,4,4,3]
```

### Example Output

```
Output: true
```

### Explanation

The given binary tree is symmetric:

```
        1
       / \
      2   2
     / \ / \
    3  4 4  3
```

---

## Approach

We can solve this problem using **recursive** or **iterative** approaches.

### Recursive Approach

1. **Base Case:** If both nodes are `None`, they are symmetric.
2. **Mismatch:** If only one node is `None` or their values differ, return `False`.
3. **Recursive Check:** Recursively compare the left subtree of one node with the right subtree of the other, and vice versa.

---

## Solution (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def isSymmetric(root: TreeNode) -> bool:
    if not root:
        return True

    def isMirror(t1, t2):
        if not t1 and not t2:
            return True
        if not t1 or not t2:
            return False
        return (t1.val == t2.val) and isMirror(t1.left, t2.right) and isMirror(t1.right, t2.left)

    return isMirror(root.left, root.right)
```

---

## Detailed Explanation

1. **Input:** `root = [1,2,2,3,4,4,3]`
2. **Recursive Calls:**
    - Compare `root.left` (2) with `root.right` (2).
    - Compare `2.left` (3) with `2.right` (3).
    - Compare `2.right` (4) with `2.left` (4).
3. **Result:** All comparisons match, so the tree is symmetric.

---

## Complexity Analysis

### Time Complexity: O(N)

- **Explanation:** Each node is visited once, leading to linear complexity.

### Space Complexity: O(H)

- **Explanation:** Recursive stack depth is proportional to the tree height (`H`). In the worst case, `H = N` for a skewed tree.

---

## Iterative Approach (Optional)

We can use a queue to perform a level-order traversal and compare nodes iteratively.

```python
from collections import deque

def isSymmetric(root: TreeNode) -> bool:
    if not root:
        return True

    queue = deque([(root.left, root.right)])

    while queue:
        t1, t2 = queue.popleft()
        if not t1 and not t2:
            continue
        if not t1 or not t2 or t1.val != t2.val:
            return False
        queue.append((t1.left, t2.right))
        queue.append((t1.right, t2.left))

    return True
```

---

## Edge Cases

1. **Empty Tree:** `root = None` → Output: `True` (symmetric by definition).
2. **Single Node:** `root = [1]` → Output: `True`.
3. **Asymmetric Tree:** `root = [1,2,2,null,3,null,3]` → Output: `False`.

---

## Conclusion

The recursive solution provides an efficient way to check tree symmetry with linear time complexity and logarithmic space complexity for balanced trees.

---

Let me know if you'd like further clarifications or alternative approaches!