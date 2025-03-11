# 654. Maximum Binary Tree

## Problem Statement

Given an integer array `nums` with no duplicates, construct a maximum binary tree based on the following rules:

1. The root is the maximum number in `nums`.
2. The left subtree is the maximum tree constructed from elements left of the maximum value.
3. The right subtree is the maximum tree constructed from elements right of the maximum value.

Return the root node of the maximum binary tree.

## Approach

1. Identify the maximum value in the array and create a root node.
2. Recursively construct the left and right subtrees using the elements left and right of the maximum value, respectively.
3. Base case: If the array is empty, return `None`.

## Code Implementation (Python)

### Recursive Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def constructMaximumBinaryTree(nums):
        if not nums:
            return None
        
        max_index = nums.index(max(nums))
        root = TreeNode(nums[max_index])
        
        root.left = self.constructMaximumBinaryTree(nums[:max_index])
        root.right = self.constructMaximumBinaryTree(nums[max_index + 1:])
        
        return root   
```

## Time Complexity Analysis

- Each recursive call finds the maximum in the list **O(N)** and splits the list.
- In the worst case (sorted list), this results in **O(N²)** time complexity.
- In the best case (balanced partition), the complexity is **O(N log N)**.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.
- In the best case (balanced tree), `H = O(log N)`, leading to **O(log N)** space complexity.

## Conclusion

The recursive approach efficiently constructs the maximum binary tree by always selecting the largest element as the root. However, it may perform poorly on already sorted arrays due to its **O(N²)** complexity.