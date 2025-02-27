# 590. N-ary Tree Postorder Traversal

## Problem Statement

Given the `root` of an N-ary tree, return its postorder traversal. In postorder traversal, we:

1. Traverse all the children from left to right.
2. Visit the root node last.

## Approach

We can solve this problem using both recursive and iterative methods:

### Recursive Approach

1. Start from the root node.
2. Recursively traverse all the children.
3. Append the root node value to the result list.

## Code Implementation (Python)

```python
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children if children is not None else []

def postorder(root: Node) -> list[int]:
    result = []
    
    def traverse(node):
        if not node:
            return
        for child in node.children:
            traverse(child)
        result.append(node.val)
    
    traverse(root)
    return result
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
def postorder_iterative(root: Node) -> list[int]:
    if not root:
        return []
    
    stack, result = [root], []
    while stack:
        node = stack.pop()
        result.append(node.val)
        stack.extend(node.children)
    
    return result[::-1]  # Reverse the result to get the correct postorder
```

### Complexity of Iterative Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(N)** (stack holds nodes in worst case)

## Conclusion

Both recursive and iterative approaches efficiently perform postorder traversal of an N-ary tree. The iterative method avoids recursion overhead, while the recursive method is more intuitive.