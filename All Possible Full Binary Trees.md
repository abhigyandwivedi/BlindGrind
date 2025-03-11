# 894. All Possible Full Binary Trees

## Problem Statement

Given an integer `n`, return all possible **full binary trees** with `n` nodes.

- A full binary tree is a tree where every node has **0 or 2 children**.
- Return the answer as a list of root nodes of the trees.

## Approach

1. If `n` is even, return an empty list since a full binary tree must have an **odd** number of nodes.
2. Use recursion to construct all possible full binary trees:
    - The root node is always present.
    - The left and right subtrees split the remaining `n-1` nodes.
    - Iterate through all possible left subtree sizes and recursively build left and right subtrees.
3. Use **memoization** (via a dictionary) to store results for each `n` to avoid redundant calculations.

## Code Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def allPossibleFBT(n):
    if n % 2 == 0:
        return []  # Full binary trees must have an odd number of nodes
    
    memo = {}  # Dictionary for memoization

    def generate_trees(nodes, memo):
        if nodes == 1:
            return [TreeNode(0)]
        if nodes in memo:
            return memo[nodes]
        
        result = []
        for left_nodes in range(1, nodes, 2):
            right_nodes = nodes - 1 - left_nodes
            for left_subtree in generate_trees(left_nodes, memo):
                for right_subtree in generate_trees(right_nodes, memo):
                    root = TreeNode(0, left_subtree, right_subtree)
                    result.append(root)
        
        memo[nodes] = result  # Store computed results
        return result
    
    return generate_trees(n, memo)

```
## Time Complexity Analysis

- The number of possible full binary trees grows **exponentially**.
- Recursion splits nodes into left and right subtrees, leading to **O(2^N)** complexity.
- Memoization significantly reduces redundant calculations, optimizing performance.

## Space Complexity Analysis

- **O(N)** recursion depth in the worst case.
- **O(2^N)** space for storing all unique trees.

## Conclusion

This approach efficiently generates all possible full binary trees using recursion and dictionary-based memoization. The time complexity is exponential, but memoization helps optimize the solution.