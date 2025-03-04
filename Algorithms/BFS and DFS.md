```markdown
# Level Order Traversal of a Binary Tree

## Introduction
Level Order Traversal is a technique to traverse a binary tree level by level from top to bottom. We use a queue (FIFO structure) to achieve this.

## Algorithm
1. **Start with the root node**: Push it into the queue.
2. **While the queue is not empty**:
   - Remove the front node.
   - Print its value.
   - Add its left child to the queue (if exists).
   - Add its right child to the queue (if exists).
3. **Repeat** until all nodes are visited.

---

## Implementation in Python

```python
from collections import deque

class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
    
    def level_order_traversal(self,root):
        if not root:
            return []
        queue=deque([root])
        result=[]
        while queue:
            level_size=len(queue)
            current_level=[]
            for _ in range(level_size):
                node=queue.popleft()
                current_level.append(node.value)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            result.append(current_level)
        return result    
    
if __name__=="__main__" :
    root=TreeNode(1)
    root.left=TreeNode(2)
    root.right=TreeNode(3)
    root.left.left=TreeNode(4)
    root.left.right=TreeNode(5)
    root.right.left=TreeNode(6)
    root.right.right=TreeNode(7)
    print(root.level_order_traversal(root))

```

## Explanation Level-wise
- **Level 1**: [1] → Root node.
- **Level 2**: [2, 3] → Left and right child of root.
- **Level 3**: [4, 5, 6, 7] → Children of nodes 2 and 3.

## Output
```
[[1], [2, 3], [4, 5, 6, 7]]
```

## Complexity Analysis
- **Time Complexity**: \(O(N)\), since each node is visited once.
- **Space Complexity**: \(O(N)\), as we use a queue to store nodes.

## Conclusion
Level Order Traversal helps in BFS-based tree processing, such as finding the depth, width, or printing nodes at each level.

---

## Recursive Approach
### Algorithm
1. **Find the height** of the tree.
2. **Print nodes at each level recursively** using a helper function.

```python
def tree_height(root):
    if not root:
        return 0
    return 1 + max(tree_height(root.left), tree_height(root.right))

def print_level(root, level, result):
    if not root:
        return
    if level == 1:
        result.append(root.value)
    else:
        print_level(root.left, level - 1, result)
        print_level(root.right, level - 1, result)

def level_order_recursive(root):
    height = tree_height(root)
    result = []
    for i in range(1, height + 1):
        level_result = []
        print_level(root, i, level_result)
        result.append(level_result)
    return result

# Example Usage
if __name__ == "__main__":
    print(level_order_recursive(root))
```

### Complexity Analysis
- **Time Complexity**: \(O(N^2)\) in the worst case (due to repeated traversal for each level).
- **Space Complexity**: \(O(N)\) for recursion stack in case of a skewed tree.

---



***********************************

# Depth First Search (DFS) Traversal of a Binary Tree

## Introduction
DFS is a traversal technique that explores as far as possible along each branch before backtracking.

## Types of DFS Traversal
1. **Preorder (Root, Left, Right)**
2. **Inorder (Left, Root, Right)**
3. **Postorder (Left, Right, Root)**

---

## Recursive Approach
```python
def dfs_recursive_preorder(root):
    if not root:
        return []
    return [root.value] + dfs_recursive_preorder(root.left) + dfs_recursive_preorder(root.right)

def dfs_recursive_inorder(root):
    if not root:
        return []
    return dfs_recursive_inorder(root.left) + [root.value] + dfs_recursive_inorder(root.right)

def dfs_recursive_postorder(root):
    if not root:
        return []
    return dfs_recursive_postorder(root.left) + dfs_recursive_postorder(root.right) + [root.value]
```

## Iterative Approach
```python
def dfs_iterative_preorder(root):
    if not root:
        return []
    stack, result = [root], []
    while stack:
        node = stack.pop()
        result.append(node.value)
        if node.right:
            stack.append(node.right)
        if node.left:
            stack.append(node.left)
    return result

def dfs_iterative_inorder(root):
    stack, result = [], []
    current = root
    while stack or current:
        if current:
            stack.append(current)
            current = current.left
        else:
            current = stack.pop()
            result.append(current.value)
            current = current.right
    return result

def dfs_iterative_postorder(root):
    if not root:
        return []
    stack, result = [root], []
    while stack:
        node = stack.pop()
        result.append(node.value)
        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)
    return result[::-1]  # Reverse to get postorder
```

## Complexity Analysis
- **Time Complexity**: \(O(N)\) for all approaches, as every node is visited once.
- **Space Complexity**:
  - **Recursive**: \(O(N)\) in the worst case due to recursion stack.
  - **Iterative**: \(O(N)\) in the worst case due to stack usage.

## Conclusion
DFS is useful for tree traversal, topological sorting, and graph traversal applications.
