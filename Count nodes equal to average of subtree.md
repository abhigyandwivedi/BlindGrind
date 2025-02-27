# 2265. Count Nodes Equal to Average of Subtree

## Problem Statement

Given the `root` of a binary tree, return the number of nodes where the value of the node is equal to the average of the values in its subtree.

- A subtree of `node` consists of `node` and all its descendants.
- The average is the sum of the values in the subtree divided by the number of nodes in the subtree.

## Approach

1. Use Depth-First Search (DFS) to traverse the tree.
2. For each node, compute the sum and count of nodes in its subtree.
3. Check if the node’s value is equal to the computed average.
4. Maintain a counter to track the number of such nodes.

## Code Implementation (Python)

### Recursive DFS Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def countNodesEqualToSubtreeAverage(root: TreeNode) -> int:
    count = 0
    
    def dfs(node):
        nonlocal count
        if not node:
            return (0, 0)  # (sum, count)
        
        left_sum, left_count = dfs(node.left)
        right_sum, right_count = dfs(node.right)
        
        total_sum = left_sum + right_sum + node.val
        total_count = left_count + right_count + 1
        
        if node.val == total_sum // total_count:  # Integer division
            count += 1
        
        return (total_sum, total_count)
    
    dfs(root)
    return count
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.

## Conclusion

The DFS approach efficiently computes the sum and count of nodes in each subtree to determine if the node’s value matches the average. The solution runs in **O(N) time** with **O(H) space** due to recursion.