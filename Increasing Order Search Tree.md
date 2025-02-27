# 897. Increasing Order Search Tree

## Problem Statement

Given the `root` of a binary search tree, rearrange the tree in increasing order so that the leftmost node becomes the new root, and each node only has a right child.

## Approach

To achieve this, we perform an in-order traversal to collect nodes in sorted order and then reattach them in a right-skewed manner:

1. Use in-order traversal (left-root-right) to retrieve nodes in sorted order.
2. Create a new tree with only right children using the sorted nodes.
3. Return the new root.

## Code Implementation (Python)

### Recursive Approach

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def increasingBST(root: TreeNode) -> TreeNode:
    def inorder(node):
        if not node:
            return []
        return inorder(node.left) + [node] + inorder(node.right)
    
    nodes = inorder(root)
    
    for i in range(len(nodes) - 1):
        nodes[i].left = None
        nodes[i].right = nodes[i + 1]
    
    nodes[-1].left = nodes[-1].right = None
    return nodes[0]
```

## Time Complexity Analysis

- In-order traversal takes **O(N)** time.
- Rearranging the nodes also takes **O(N)** time.
- Overall, the complexity is **O(N)**.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the tree height.
- The extra list `nodes` takes **O(N)** space.
- In total, space complexity is **O(N)**.

## Alternative Approach: In-place Traversal with Dummy Node

Instead of storing nodes in a list, we can use a dummy node to construct the result tree in-place.

```python
def increasingBST_inplace(root: TreeNode) -> TreeNode:
    def inorder(node):
        nonlocal curr
        if not node:
            return
        inorder(node.left)
        node.left = None
        curr.right = node
        curr = node
        inorder(node.right)
    
    dummy = TreeNode()
    curr = dummy
    inorder(root)
    return dummy.right
```

### Complexity of In-place Approach

- **Time Complexity**: **O(N)** (each node is visited once)
- **Space Complexity**: **O(H)** (recursion stack only, no extra list)

## Conclusion

Both approaches efficiently rearrange the BST into an increasing order search tree. The in-place approach is more space-efficient, while the first approach is more intuitive.