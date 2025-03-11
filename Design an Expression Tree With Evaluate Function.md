# 1628. Design an Expression Tree With Evaluate Function

## Problem Statement

Implement an **Expression Tree** that supports evaluating postfix expressions.

- You are given a list of **strings** representing a postfix expression.
- The expression tree should be built using the given postfix notation.
- Each node in the tree represents an **operator** (`+`, `-`, `*`, `/`) or an **operand** (integer).
- The tree's root node should return the result when calling `.evaluate()`.

## Approach

1. **Use a stack to construct the expression tree**
    
    - Since postfix notation means operators come **after** operands, we can use a stack to process elements efficiently.
    - When encountering an operand (integer), we push it onto the stack as a `TreeNode`.
    - When encountering an operator (`+`, `-`, `*`, `/`), we pop the top two nodes from the stack, make them its children, and push the new subtree back onto the stack.
    - The final element in the stack is the root of the expression tree.
2. **Implement a base `Node` class with an `evaluate()` method**
    
    - This interface ensures that each node (whether operator or operand) can be evaluated consistently.
3. **Implement `OperandNode` and `OperatorNode`**
    
    - `OperandNode`: Represents numbers and simply returns its stored value when evaluated.
    - `OperatorNode`: Represents an operator and evaluates its left and right subtrees before applying the operation.
4. **Build the tree using `TreeBuilder`**
    
    - The `buildTree()` method processes the postfix expression and constructs the expression tree.


```python
import abc
from abc import ABCMeta, abstractmethod

"""
This is the interface for the expression tree Node.
You should not remove it, and you can define some classes to implement it.
"""

class Node:
    __metaclass__ = ABCMeta
    @abstractmethod
    def evaluate(self):
        pass

# Concrete class for operand nodes (numbers)
class OperandNode(Node):
    def __init__(self, value):
        self.value = int(value)

    def evaluate(self):
        return self.value

# Concrete class for operator nodes (+, -, *, /)
class OperatorNode(Node):
    def __init__(self, operator, left, right):
        self.operator = operator
        self.left = left
        self.right = right

    def evaluate(self):
        left_val = self.left.evaluate()
        right_val = self.right.evaluate()

        if self.operator == "+":
            return left_val + right_val
        elif self.operator == "-":
            return left_val - right_val
        elif self.operator == "*":
            return left_val * right_val
        elif self.operator == "/":
            return left_val // right_val  # Integer division

"""    
This is the TreeBuilder class.
You can treat it as the driver code that takes the postfix input
and returns the expression tree representing it as a Node.
"""

class TreeBuilder(object):
    def buildTree(self, postfix):
        """
        :type postfix: List[str]
        :rtype: Node
        """
        stack = []

        for token in postfix:
            if token.isdigit():  # If it's an operand (number)
                stack.append(OperandNode(token))
            else:  # It's an operator
                right = stack.pop()
                left = stack.pop()
                stack.append(OperatorNode(token, left, right))

        return stack[0]  # Root of the expression tree

"""
Your TreeBuilder object will be instantiated and called as such:
obj = TreeBuilder();
expTree = obj.buildTree(postfix);
ans = expTree.evaluate();
"""

```

## Explanation

### **Building the Expression Tree**

Given a postfix expression list like:
["3", "4", "+", "2", "*", "7", "/"]

The construction follows these steps:

1. Push `3` onto the stack → Stack: `[3]`
2. Push `4` onto the stack → Stack: `[3, 4]`
3. Encounter `+`, pop `4` and `3`, create `+` node → Stack: `[+ (3, 4)]`
4. Push `2` onto the stack → Stack: `[+ (3, 4), 2]`
5. Encounter `*`, pop `2` and `+ (3,4)`, create `*` node → Stack: `[* (+ (3, 4), 2)]`
6. Push `7` onto the stack → Stack: `[* (+ (3, 4), 2), 7]`
7. Encounter `/`, pop `7` and `* (+ (3,4),2)`, create `/` node → Stack: `[/ (* (+ (3, 4), 2), 7)]`

The final tree structure:

      (/)
     /   \
   (*)     7
  /   \
(+)     2
/   \
3     4

### **Evaluating the Expression**

The `evaluate()` function is called on the root `/` node:

1. `+` node evaluates to `3 + 4 = 7`
2. `*` node evaluates to `7 * 2 = 14`
3. `/` node evaluates to `14 // 7 = 2`

Final result: **2**

## **Time Complexity Analysis**

1. **Building the tree:**
    - Each token is processed once → **O(N)**
    - Stack operations (push/pop) take constant time → **O(1) per operation**
    - **Total: O(N)**
2. **Evaluating the tree:**
    - Each node is visited once (postorder traversal) → **O(N)**

### **Overall Complexity:** **O(N)**

---

## **Space Complexity Analysis**

- **O(N)** for the stack used during tree construction.
- **O(N)** for storing the expression tree nodes.
- **Total: O(N)**

---

## Conclusion

- The approach efficiently builds an expression tree from a postfix expression.
- The `evaluate()` method correctly computes the result using recursion.
- The solution runs in **O(N) time** and uses **O(N) space**.

This design ensures that the expression tree can handle large postfix expressions efficiently. 🚀