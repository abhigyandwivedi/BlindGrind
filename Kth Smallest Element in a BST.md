# Solution to "230. Kth Smallest Element in a BST"

## Problem Statement

Given the root of a binary search tree (BST) and an integer `k`, return the `k`th smallest value (1-indexed) of all the values of the nodes in the tree.

---

## Approach: Inorder Traversal

### Explanation

1. **Inorder Traversal:** In a BST, an inorder traversal (left → root → right) visits nodes in ascending order.
2. **Count Nodes:** Traverse the tree while keeping track of the count of nodes visited.
3. **Stop at kth Node:** Once the `k`th node is reached, return its value.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        self.count = 0
        self.result = None

        def inorder(node):
            if not node or self.result is not None:
                return

            inorder(node.left)
            self.count += 1

            if self.count == k:
                self.result = node.val
                return

            inorder(node.right)

        inorder(root)
        return self.result
```

---

## Example Run

Input:

```python
root = TreeNode(3)
root.left = TreeNode(1)
root.right = TreeNode(4)
root.left.right = TreeNode(2)

solution = Solution()
print(solution.kthSmallest(root, 2))
```

Output:

```
2
```

Explanation:

- The inorder traversal sequence is `[1, 2, 3, 4]`.
- The 2nd smallest element is `2`.

---

## Complexity Analysis

1. **Time Complexity:** `O(H + k)`
    
    - `H` is the height of the tree.
    - In the worst case (skewed tree), `H` can be `O(n)`.
2. **Space Complexity:** `O(H)`
    
    - Recursive stack space.

---

## Edge Cases

1. `k = 1` → Return the smallest element.
2. `k` equals the total number of nodes → Return the largest element.

---

## Conclusion

By using an efficient inorder traversal, we find the `k`th smallest element in a BST without traversing the entire tree.