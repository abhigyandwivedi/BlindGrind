# 938. Range Sum of BST

## Problem Statement

Given the `root` of a Binary Search Tree (BST) and two integers `low` and `high`, return the sum of values of all nodes with a value in the inclusive range `[low, high]`.

## Approach

We can solve this problem using a Depth-First Search (DFS) or a Breadth-First Search (BFS). Given the properties of a BST:

- The left subtree contains only nodes with values less than the root.
- The right subtree contains only nodes with values greater than the root.

### Optimized DFS Approach

1. Traverse the BST using DFS.
2. If the current node value is within `[low, high]`, add it to the sum.
3. If the current node value is greater than `low`, recursively search the left subtree.
4. If the current node value is less than `high`, recursively search the right subtree.
5. Return the total sum.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def rangeSumBST(root: TreeNode, low: int, high: int) -> int:
    if not root:
        return 0
    
    total_sum = 0
    if low <= root.val <= high:
        total_sum += root.val
    
    if root.val > low:
        total_sum += rangeSumBST(root.left, low, high)
    
    if root.val < high:
        total_sum += rangeSumBST(root.right, low, high)
    
    return total_sum
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the BST.
- The function does not traverse unnecessary branches, making it more efficient in balanced BSTs.

## Space Complexity Analysis

- The space complexity is **O(H)**, where `H` is the height of the tree.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.
- In a balanced BST, `H = O(log N)`, leading to **O(log N)** space complexity.

## Alternative Approach: Iterative DFS (Using Stack)

Instead of recursion, we can use a stack to implement an iterative DFS approach.

```python
def rangeSumBST_iterative(root: TreeNode, low: int, high: int) -> int:
    stack = [root]
    total_sum = 0
    
    while stack:
        node = stack.pop()
        if node:
            if low <= node.val <= high:
                total_sum += node.val
            if node.val > low:
                stack.append(node.left)
            if node.val < high:
                stack.append(node.right)
    
    return total_sum
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is visited once)
- **Space Complexity**: **O(H)** (stack stores at most `H` nodes, where `H` is the tree height)

## Conclusion

Both recursive and iterative DFS solutions efficiently compute the range sum in a BST. The recursive approach is concise, while the iterative approach avoids function call overhead.