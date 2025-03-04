# 1302. Deepest Leaves Sum

## Problem Statement

Given the `root` of a binary tree, return the sum of values of its deepest leaves.

## Approach

1. Perform a level-order traversal (BFS) to find the deepest level of the tree.
2. Sum the values of all nodes at the deepest level.

## Code Implementation (Python)

### BFS Approach

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def deepestLeavesSum(root: TreeNode) -> int:
    if not root:
        return 0
    
    queue = deque([root])
    
    while queue:
        level_sum = 0
        for _ in range(len(queue)):
            node = queue.popleft()
            level_sum += node.val
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    
    return level_sum
```

## Time Complexity Analysis

- Each node is visited once, leading to **O(N)** complexity, where `N` is the number of nodes in the tree.

## Space Complexity Analysis

- The queue holds at most one level of nodes, so in the worst case, it stores **O(N)** nodes (for a balanced tree, it's **O(N/2) ≈ O(N)** in the last level).

## Alternative Approach: DFS

Instead of BFS, we can use DFS to keep track of the maximum depth and sum values at that depth.

```python
def deepestLeavesSum_DFS(root: TreeNode) -> int:
    max_depth = 0
    total_sum = 0
    
    def dfs(node, depth):
        nonlocal max_depth, total_sum
        if not node:
            return
        
        if depth > max_depth:
            max_depth = depth
            total_sum = node.val
        elif depth == max_depth:
            total_sum += node.val
        
        dfs(node.left, depth + 1)
        dfs(node.right, depth + 1)
    
    dfs(root, 0)
    return total_sum
```

### Complexity of DFS Approach

- **Time Complexity**: **O(N)** (each node is processed once)
- **Space Complexity**: **O(H)** (recursion stack, where `H` is tree height, worst case **O(N)** for a skewed tree)

## Conclusion

Both BFS and DFS approaches efficiently calculate the sum of the deepest leaves. BFS naturally finds the last level, while DFS explicitly tracks the maximum depth.



# Depth-First Search (DFS) to Find the Last Level of a Binary Tree

## Overview

Depth-First Search (DFS) is a traversal technique that explores as far as possible along a branch before backtracking. When applied to a binary tree, DFS helps in:

1. **Finding the maximum depth (height) of the tree.**
2. **Collecting nodes at the deepest level.**

This method efficiently finds the last level of the tree using recursion.

---

## Steps to Find the Last Level Using DFS

### **1. Find the Depth (Height) of the Tree**

The depth of a binary tree is the longest path from the root to a leaf node.

- Recursively calculate the depth of the left and right subtrees.
- The maximum of these values plus one gives the depth of the current node.

#### **Python Implementation:**

```python
# Function to find the maximum depth of the tree
def find_depth(root):
    if not root:
        return 0
    return 1 + max(find_depth(root.left), find_depth(root.right))
```

**Time Complexity:**

- Each node is visited **once**, making it **O(N)** for **N** nodes.

**Space Complexity:**

- Recursive stack depth is at most **O(H)**, where **H** is the height of the tree.

---

### **2. Collect Nodes at the Deepest Level**

Once we have the maximum depth, we traverse again and collect nodes at that depth.

- Recursively explore the left and right subtrees.
- If the current level matches the maximum depth, store the node's value.

#### **Python Implementation:**

```python
# Function to collect nodes at the maximum depth
def collect_last_level(root, level, max_depth, result):
    if not root:
        return
    if level == max_depth:
        result.append(root.val)
    collect_last_level(root.left, level + 1, max_depth, result)
    collect_last_level(root.right, level + 1, max_depth, result)
```

**Time Complexity:**

- Again, each node is visited **once**, making it **O(N)**.

**Space Complexity:**

- In the worst case, the recursion stack reaches **O(H)**.

---

### **3. Combining Both Steps in a Single Function**

The function `find_last_level_dfs` performs the entire process:

1. Finds the tree's depth.
2. Collects all nodes at the last level.

#### **Python Implementation:**

```python
def find_last_level_dfs(root):
    max_depth = find_depth(root)  # Step 1: Find maximum depth
    result = []
    collect_last_level(root, 1, max_depth, result)  # Step 2: Collect nodes at last level
    return result
```

---

## Example Usage

```python
# Example Tree:
#         1
#       /   \
#      2     3
#     / \     \
#    4   5     6
#             /
#            7

root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
root.left.right = TreeNode(5)
root.right.right = TreeNode(6)
root.right.right.left = TreeNode(7)

print(find_last_level_dfs(root))  # Output: [4, 5, 7]
```

---

## Why Use DFS for This Problem?

✅ **Efficient in space usage** (uses recursion stack instead of queue). ✅ **Two-pass approach works well for balanced and unbalanced trees.** ✅ **Recursive structure aligns naturally with tree traversal.**

---

## Time & Space Complexity Summary

|Operation|Time Complexity|Space Complexity|
|---|---|---|
|Finding depth|O(N)|O(H)|
|Collecting last level|O(N)|O(H)|
|**Total**|**O(N)**|**O(H)**|

Where **N** is the number of nodes and **H** is the height of the tree.

---

## Conclusion

Depth-First Search is a powerful technique for finding the last level of a binary tree. By first determining the tree's depth and then collecting nodes at that depth, we ensure an efficient **O(N)** traversal while maintaining a **O(H)** space complexity, which is optimal for trees with limited height.

```python
from tree_node import TreeNode

def depth_of_tree(root):
     if not root:
        return 0
     return 1+max(depth_of_tree(root.left),depth_of_tree(root.right))
def collect_last_level(root,level,max_level,result):
    if not root:
        return 
    if level==max_level:
        result.append(root)
    collect_last_level(root.left,level+1,max_level,result)    
    collect_last_level(root.right,level+1,max_level,result)

def last_level_list(root):
    result=[]
    max_depth=depth_of_tree(root)
    collect_last_level(root,1,max_depth,result)
    return result
    


if __name__=="__main__" :
    root=TreeNode(1)
    root.left=TreeNode(2)
    root.right=TreeNode(3)
    root.left.left=TreeNode(4)
    root.left.right=TreeNode(5)
    root.right.left=TreeNode(6)
    root.right.right=TreeNode(7)
    root.right.right.right=TreeNode(8)
    nodes=last_level_list(root)
    print(sum(node.value for node in nodes))

```