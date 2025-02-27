# 1628. Design an Expression Tree With Evaluate Function

## Problem Statement

Design an expression tree where each node is an operator (`+`, `-`, `*`, `/`) or an operand (integer). Implement an `evaluate()` function that computes the result of the expression represented by the tree.

## Approach

1. Each node of the tree is either an operator or an operand.
2. Operators have exactly two children (binary tree structure).
3. Operands are leaf nodes with integer values.
4. Use a recursive `evaluate()` function to compute the result:
    - If the node is a number, return its value.
    - If the node is an operator, evaluate the left and right children and apply the operator.

## Code Implementation (Python)

### Class Definitions

```python
class TreeNode:
    def __init__(self, val="", left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class ExpressionTree:
    def __init__(self, root: TreeNode):
        self.root = root
    
    def evaluate(self) -> int:
        return self._evaluate_node(self.root)
    
    def _evaluate_node(self, node: TreeNode) -> int:
        if not node.left and not node.right:
            return int(node.val)  # Leaf node (operand)
        
        left_val = self._evaluate_node(node.left)
        right_val = self._evaluate_node(node.right)
        
        if node.val == '+':
            return left_val + right_val
        elif node.val == '-':
            return left_val - right_val
        elif node.val == '*':
            return left_val * right_val
        elif node.val == '/':
            return left_val // right_val  # Integer division
        
        raise ValueError("Invalid operator")
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The recursion stack takes **O(H)** space, where `H` is the height of the tree.
- In a balanced tree, **O(log N)** space is used.
- In the worst case (skewed tree), **O(N)** space is required.

## Conclusion

The recursive approach efficiently evaluates an expression tree in **O(N) time** with **O(H) space** due to recursion. This design ensures correct evaluation of arithmetic expressions using a binary tree representation.