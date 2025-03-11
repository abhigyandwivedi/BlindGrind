# 1038. Binary Search Tree to Greater Sum Tree

## Problem Statement

Given the `root` of a Binary Search Tree (BST), convert it into a Greater Sum Tree (GST) where each node's value is replaced by the sum of all values greater than or equal to it.

## Approach

1. Perform a reverse in-order traversal (right -> root -> left) to accumulate sums.
2. Maintain a running sum while traversing, updating each node's value.
3. Continue updating the nodes recursively or iteratively.

## Code Implementation (Python)

### Recursive Approach 

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def binaryTreeToGst(root: TreeNode) -> TreeNode:
        def reverse_inorder(node, total):
            if node is None:
                return total  # Return the updated total sum
            
            # Process the right subtree first
            total = reverse_inorder(node.right, total)
            
            # Update the current node value
            node.val += total
            total = node.val  # Update total to the new node value
            
            # Process the left subtree
            return reverse_inorder(node.left, total)

        reverse_inorder(root, 0)  # Start traversal with sum = 0
        return root

```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, `H = O(log N)`, leading to **O(log N)** space complexity.
- In the worst case (skewed tree), `H = O(N)`, leading to **O(N)** space complexity.

## Alternative Approach: Iterative Using Stack

Instead of recursion, we can use a stack to process nodes iteratively:

```python
def bstToGst_iterative(root: TreeNode) -> TreeNode:
    total_sum = 0
    stack = []
    node = root
    
    while stack or node:
        while node:
            stack.append(node)
            node = node.right
        
        node = stack.pop()
        total_sum += node.val
        node.val = total_sum
        
        node = node.left
    
    return root
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(H)** (stack holds nodes in worst case, **O(N)** for skewed trees)

## Conclusion

Both recursive and iterative approaches efficiently transform the BST into a Greater Sum Tree. The iterative method avoids recursion depth issues, while the recursive approach is more intuitive.