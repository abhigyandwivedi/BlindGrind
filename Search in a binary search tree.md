# 700. Search in a Binary Search Tree

## Problem Statement

Given the `root` of a Binary Search Tree (BST) and an integer `val`, return the node where `node.val == val`. If the value does not exist in the BST, return `None`.

## Approach

Since we are given a BST, we can leverage its properties to efficiently search for the target value:

1. If the current node is `None`, return `None`.
2. If `node.val` equals `val`, return the current node.
3. If `val` is smaller than `node.val`, search in the left subtree.
4. If `val` is greater than `node.val`, search in the right subtree.
5. Recursively or iteratively traverse until the target node is found or a `None` is reached.

## Code Implementation (Python)

### Recursive Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def searchBST(root: TreeNode, val: int) -> TreeNode:
    if not root or root.val == val:
        return root
    
    if val < root.val:
        return searchBST(root.left, val)
    else:
        return searchBST(root.right, val)
```

## Time Complexity Analysis

- Each step eliminates half of the tree, leading to **O(log N)** complexity in a balanced BST.
- In the worst case (skewed tree), it degrades to **O(N)**.

## Space Complexity Analysis

- The space complexity is **O(H)**, where `H` is the height of the tree due to recursion.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)` space complexity.
- In a skewed tree, `H = O(N)`, leading to **O(N)** space complexity.

## Alternative Approach: Iterative

An iterative approach avoids recursion overhead by using a loop.

```python
def searchBST_iterative(root: TreeNode, val: int) -> TreeNode:
    while root:
        if root.val == val:
            return root
        elif val < root.val:
            root = root.left
        else:
            root = root.right
    return None
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(log N)** in a balanced BST, **O(N)** in a skewed BST.
- **Space Complexity**: **O(1)** (no recursive call stack).

## Conclusion

Both recursive and iterative approaches efficiently search for a value in a BST. The iterative approach is more space-efficient, while the recursive approach is more intuitive.