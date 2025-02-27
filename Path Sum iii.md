# Solution to "437. Path Sum III"

## Problem Statement

Given the `root` of a binary tree and an integer `targetSum`, return the number of paths where the sum of the values along the path equals `targetSum`.

- The path does not need to start or end at the root or a leaf.
- The path only needs to move downwards (from parent nodes to child nodes).

---

## Approach: Prefix Sum + Recursion

### Explanation

We can solve this problem efficiently using a **prefix sum** approach with recursion. The key idea is to use a hashmap to store the prefix sums and count paths efficiently.

1. **Prefix Sum Definition:**
    
    - Prefix sum represents the sum of all node values from the root to the current node.
2. **Recursive Traversal:**
    
    - Traverse the tree while keeping track of the prefix sum.
    - For each node, calculate the current prefix sum.
    - Check how many times `(current_prefix_sum - targetSum)` has occurred. This indicates valid paths ending at the current node.
    - Update the prefix sum hashmap and recursively process left and right subtrees.
    - Backtrack by removing the current node's prefix sum count after recursion.

---

## Implementation in Python

```python
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> int:
        from collections import defaultdict

        def dfs(node, current_sum):
            if not node:
                return 0

            # Update the current prefix sum
            current_sum += node.val

            # Count the paths that end at the current node
            path_count = prefix_sum_count[current_sum - targetSum]

            # Update the prefix sum count for the current node
            prefix_sum_count[current_sum] += 1

            # Recurse for left and right children
            path_count += dfs(node.left, current_sum)
            path_count += dfs(node.right, current_sum)

            # Backtrack by removing the current node's contribution
            prefix_sum_count[current_sum] -= 1

            return path_count

        # Dictionary to store prefix sums and their counts
        prefix_sum_count = defaultdict(int)
        prefix_sum_count[0] = 1

        return dfs(root, 0)
```

---

## Example Run

Input:

```python
root = TreeNode(10)
root.left = TreeNode(5)
root.right = TreeNode(-3)
root.left.left = TreeNode(3)
root.left.right = TreeNode(2)
root.right.right = TreeNode(11)
root.left.left.left = TreeNode(3)
root.left.left.right = TreeNode(-2)
root.left.right.right = TreeNode(1)

targetSum = 8

solution = Solution()
print(solution.pathSum(root, targetSum))
```

Output:

```
3
```

Explanation: The 3 paths that sum to 8 are:

1. 5 → 3
2. 5 → 2 → 1
3. -3 → 11

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - Each node is visited once, and the prefix sum lookup takes constant time.
2. **Space Complexity:** `O(N)`
    
    - The recursion stack can go as deep as the height of the tree.
    - The hashmap stores prefix sums for each node.

---

## Edge Cases

1. If the tree is empty (`root = None`), return `0`.
2. If all node values are negative, the approach still works.
3. If `targetSum = 0`, paths with sum `0` are counted.

---

## Conclusion

Using the prefix sum technique allows us to efficiently find all paths with the given sum in linear time complexity. This approach ensures optimal performance even for large trees.