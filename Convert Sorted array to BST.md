# 108. Convert Sorted Array to Binary Search Tree

## Problem Statement

Given an integer array `nums` where the elements are sorted in **ascending order**, convert it to a **height-balanced** binary search tree (BST).

### Example

**Input:**

```
nums = [-10, -3, 0, 5, 9]
```

**Output:**

```
[0, -3, 9, -10, null, 5]
```

**Explanation:** One possible height-balanced BST is:

```
        0
       / \
     -3   9
     /   /
   -10  5
```

---

## Approach: Recursive Divide and Conquer

### Idea

To create a height-balanced BST:

1. Select the middle element of the array as the root.
2. Recursively build the left subtree using the left half of the array.
3. Recursively build the right subtree using the right half of the array.

Choosing the middle element ensures that the tree remains balanced.

---

## Implementation (Python)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def sortedArrayToBST(nums):
    if not nums:
        return None

    # Find the middle element
    mid = len(nums) // 2

    # Create the root node with the middle element
    root = TreeNode(nums[mid])

    # Recursively build left and right subtrees
    root.left = sortedArrayToBST(nums[:mid])
    root.right = sortedArrayToBST(nums[mid + 1:])

    return root
```

---

## Example Run

For `nums = [-10, -3, 0, 5, 9]`:

1. Middle element `0` becomes the root.
2. Left subtree is built from `[-10, -3]`.
3. Right subtree is built from `[5, 9]`.

Resulting BST:

```
        0
       / \
     -3   9
     /   /
   -10  5
```

---

## Complexity Analysis

### Time Complexity

- **O(n):** Each element is processed once to construct the tree.

### Space Complexity

- **O(log n):** Recursive stack depth for a balanced BST is proportional to the tree height, which is `O(log n)`.

---

## Edge Cases

1. `nums = []` → Output: `None` (Empty tree).
2. `nums = [1]` → Output: `Tree with a single node 1`.
3. `nums = [1, 2]` → Output: Root `1` with right child `2`.

---

## Conclusion

This solution efficiently converts a sorted array into a height-balanced BST using a recursive divide-and-conquer approach. It ensures optimal height and efficient traversal.