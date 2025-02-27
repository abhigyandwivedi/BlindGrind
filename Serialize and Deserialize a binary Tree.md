# Solution to "297. Serialize and Deserialize Binary Tree"

## Problem Statement

Design an algorithm to serialize and deserialize a binary tree. Serialization is converting a tree into a string, and deserialization is reconstructing the tree from that string.

Example:

```
Input:
    1
   / \
  2   3
     / \
    4   5
Output (Serialization): "1,2,null,null,3,4,null,null,5,null,null"
```

---

## Approach: Depth-First Search (DFS)

### Explanation

1. **Serialization:** Perform a pre-order traversal.
2. **Deserialization:** Rebuild using the pre-order structure.

---

## Implementation in Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Codec:
    def serialize(self, root):
        def dfs(node):
            if not node:
                result.append("null")
                return
            result.append(str(node.val))
            dfs(node.left)
            dfs(node.right)
        result = []
        dfs(root)
        return ",".join(result)

    def deserialize(self, data):
        values = iter(data.split(","))
        def dfs():
            val = next(values)
            if val == "null":
                return None
            node = TreeNode(int(val))
            node.left = dfs()
            node.right = dfs()
            return node
        return dfs()
```

---

## Example Run

Input:

```python
codec = Codec()
root = TreeNode(1, TreeNode(2), TreeNode(3, TreeNode(4), TreeNode(5)))
serialized = codec.serialize(root)
print("Serialized:", serialized)

deserialized = codec.deserialize(serialized)
print("Deserialized Root:", deserialized.val)
```

Output:

```
Serialized: "1,2,null,null,3,4,null,null,5,null,null"
Deserialized Root: 1
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - `N` is the number of nodes.
    - Each node is visited once during serialization and deserialization.
2. **Space Complexity:** `O(N)`
    
    - Storage for the output string and recursion stack.

---

## Edge Cases

1. Empty tree → Output: "null"
2. Single node → Serialized as "1,null,null"

---

## Conclusion

This solution efficiently converts a binary tree to a string and back using depth-first traversal.