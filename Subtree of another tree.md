# 572. Subtree of Another Tree

## Problem Statement

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values as `subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of that node's descendants. The tree `tree` could also be considered as a subtree of itself.

## Example

**Input:**

```
root = [3,4,5,1,2], subRoot = [4,1,2]
```

**Output:**

```
true
```

## Approach: Recursive Tree Traversal

We will solve this problem using a recursive approach. The idea is to traverse the main tree (`root`) and, for each node, check if the subtree rooted at that node is identical to `subRoot`.

### Steps

1. Traverse the `root` tree.
2. For each node in `root`, check if the subtree starting from that node is identical to `subRoot`.
3. If any subtree matches `subRoot`, return `true`.
4. If we traverse the entire tree and find no match, return `false`.

## Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def isSubtree(root: TreeNode, subRoot: TreeNode) -> bool:
    if not root:
        return False

    if isSameTree(root, subRoot):
        return True

    # Recursively check left and right subtrees
    return isSubtree(root.left, subRoot) or isSubtree(root.right, subRoot)

def isSameTree(s: TreeNode, t: TreeNode) -> bool:
    if not s and not t:
        return True
    if not s or not t:
        return False
    if s.val != t.val:
        return False

    # Recursively check left and right children
    return isSameTree(s.left, t.left) and isSameTree(s.right, t.right)
```

## Explanation

1. **`isSubtree` Function:**
    
    - Checks if `subRoot` is a subtree of `root` by recursively traversing `root`.
    - If the current node matches `subRoot` (checked by `isSameTree`), it returns `true`.
2. **`isSameTree` Function:**
    
    - Recursively compares two trees node by node.
    - If all nodes match in value and structure, returns `true`.

## Complexity Analysis

### Time Complexity

- Let `n` be the number of nodes in the `root` tree and `m` be the number of nodes in the `subRoot` tree.
- In the worst case, for each node in `root`, we check if its subtree matches `subRoot`.
- Each comparison takes `O(m)` time.
- Therefore, the total time complexity is:

O(n×m)O(n \times m)

### Space Complexity

- The space complexity is determined by the recursion stack depth.
- In the worst case (skewed tree), the recursion depth can be `O(n)`.
- Each recursive call takes constant space, so the total space complexity is:

O(n)O(n)

## Edge Cases

1. `root` is `None` but `subRoot` is not → return `false`.
2. Both `root` and `subRoot` are `None` → return `true`.
3. `root` exists, but `subRoot` is `None` → return `true` (empty tree is always a subtree).

## Conclusion

This solution efficiently checks whether one tree is a subtree of another using recursion. While the time complexity can be high in the worst case, it is generally effective for typical binary tree problems.