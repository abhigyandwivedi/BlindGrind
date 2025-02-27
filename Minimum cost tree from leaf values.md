
# 1130: Minimum Cost Tree From Leaf Values

## Problem Statement

Given an array of integers `arr`, you need to build a binary tree with the following properties:
- The leaf nodes of the tree are the elements of the array `arr`.
- The value of the tree is the sum of the product of every internal node with the maximum leaf value of its subtrees.

Your task is to find the minimum value of such a tree.

### Example 1:
Input: `arr = [6, 2, 4]`  
Output: `32`  
Explanation:  
We can construct the following binary tree:
```
        24
       /        6    8
     / \  
    2   4
```
The value of this tree is `(6 * 4) + (2 * 4) + (4 * 4) = 32`.

### Example 2:
Input: `arr = [4, 11]`  
Output: `44`

### Constraints:
- 2 <= `arr.length` <= 40
- 1 <= `arr[i] <= 15`

## Approach

To solve this problem, we need to find the minimum cost for constructing the binary tree. This is a typical problem that can be solved using **Dynamic Programming (DP)**. The key observation is to note that the minimum cost for constructing a tree can be found recursively by considering all possible binary trees with different root nodes.

### Dynamic Programming Approach:
1. **Recursive Decomposition**:
   - The problem can be broken down into a smaller subproblem: Given a subarray of `arr`, we want to find the minimum cost to construct the tree from this subarray.
   - The cost of a tree can be defined recursively as:
     - `cost(arr[i...j]) = min(cost(arr[i...k]) + cost(arr[k+1...j]) + max(arr[i...k]) * max(arr[k+1...j]))` for all `k` in the range `[i, j-1]`.

2. **Memoization**:
   - Since the problem involves overlapping subproblems, we can use **memoization** to store the results of subproblems that have already been computed.

3. **Base Case**:
   - If there is only one element in the subarray, the cost is `0`, because no internal nodes exist in the tree.

### Solution Code:

```python
def mctFromLeafValues(arr):
    n = len(arr)
    # dp[i][j] will store the minimum cost to build a tree from arr[i] to arr[j]
    dp = [[float('inf')] * n for _ in range(n)]
    # max_val[i][j] will store the maximum value in the subarray arr[i...j]
    max_val = [[0] * n for _ in range(n)]
    
    # Fill the max_val array
    for i in range(n):
        max_val[i][i] = arr[i]
        for j in range(i + 1, n):
            max_val[i][j] = max(max_val[i][j - 1], arr[j])
    
    # Base case: when there's only one element, the cost is 0
    for i in range(n):
        dp[i][i] = 0
    
    # Fill the dp array
    for length in range(2, n + 1):  # length of the subarray
        for i in range(n - length + 1):
            j = i + length - 1
            # Try every possible partition of the subarray [i...j]
            for k in range(i, j):
                dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j] + max_val[i][k] * max_val[k+1][j])
    
    return dp[0][n - 1]
```

## Explanation of the Code:

1. **Initialization**:
   - We initialize two 2D arrays:
     - `dp[i][j]`: This stores the minimum cost to construct a tree using the subarray `arr[i...j]`.
     - `max_val[i][j]`: This stores the maximum value in the subarray `arr[i...j]`.
   
2. **Filling `max_val`**:
   - The array `max_val` is filled such that `max_val[i][j]` holds the maximum value in the subarray `arr[i...j]`. This is done by iterating over all possible subarrays.

3. **Base Case**:
   - The base case for the DP is that when there is only one element in the subarray, the cost is `0` because there are no internal nodes.

4. **Recursive DP Calculation**:
   - We compute the cost for subarrays of increasing lengths (from 2 to `n`).
   - For each subarray `arr[i...j]`, we try every possible partition `k`, where the left subarray is `arr[i...k]` and the right subarray is `arr[k+1...j]`. The cost for the subarray is the sum of:
     - The cost of the left subarray: `dp[i][k]`
     - The cost of the right subarray: `dp[k+1][j]`
     - The cost for the root node formed by the left and right subarrays: `max_val[i][k] * max_val[k+1][j]`

5. **Final Answer**:
   - The final answer is stored in `dp[0][n-1]`, which gives the minimum cost to construct the binary tree from the entire array.

## Time and Space Complexity:

- **Time Complexity**: O(n^3), where `n` is the length of the `arr` array.
  - We compute the minimum cost for each subarray `arr[i...j]` and for each subarray, we try all possible partitions `k`. This leads to three nested loops.

- **Space Complexity**: O(n^2), as we use two 2D arrays (`dp` and `max_val`) to store the results of subproblems.

## Example Walkthrough:

For `arr = [6, 2, 4]`:

1. **Initialization**:
   - `max_val` array is filled to store the maximum values for all subarrays.
   - `dp` array is initialized with infinity, and the base case is set for single-element subarrays.

2. **Filling DP**:
   - We compute the minimum cost for subarrays of increasing lengths:
     - For `arr[0...1]`, we try partitioning at `k = 0`.
     - For `arr[1...2]`, we try partitioning at `k = 1`.
     - For `arr[0...2]`, we try both possible partitions at `k = 0` and `k = 1`.

3. **Final Result**:
   - The minimum cost to construct the binary tree for `arr = [6, 2, 4]` is `32`.

## Conclusion

This dynamic programming approach ensures we efficiently find the minimum cost tree while considering all possible partitions of the array. The use of memoization avoids redundant calculations, making the solution feasible even for the maximum input size.