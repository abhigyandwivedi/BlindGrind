
# 494: Target Sum

## Problem Statement

You are given a list of integers called `nums` and an integer `target`. You need to find the number of ways to assign symbols to the numbers such that their sum equals the `target`. You can assign either a `+` or a `-` symbol to each number in the list.

### Example 1:
Input: `nums = [1, 1, 1, 1, 1], target = 3`  
Output: `5`  
Explanation: There are five ways to assign symbols to the numbers such that their sum equals 3:
- `+1 +1 +1 -1 -1 = 3`
- `+1 +1 -1 +1 -1 = 3`
- `+1 +1 -1 -1 +1 = 3`
- `+1 -1 +1 +1 -1 = 3`
- `-1 +1 +1 +1 -1 = 3`

### Example 2:
Input: `nums = [1], target = 1`  
Output: `1`  
Explanation: There is only one way to assign symbols to the numbers such that their sum equals 1: `+1`.

### Constraints:
- 1 <= `nums.length` <= 20
- 0 <= `nums[i] <= 1000`
- `-1000 <= target <= 1000`

## Approach

This problem can be efficiently solved using **Dynamic Programming (DP)** by recognizing that the problem has a subset-sum property. The key idea is to translate the problem of finding the number of ways to reach a target sum into a subset-sum problem by transforming the problem into partitioning the numbers into two subsets.

### Key Insights:
1. **Transformation**:
   - The problem asks to assign `+` and `-` signs to each number. If we consider the sum of all numbers in the list as `S`, then the problem becomes finding two subsets:
     - Subset 1: the subset of numbers with `+` signs.
     - Subset 2: the subset of numbers with `-` signs.
   - The sum of the numbers with a `+` sign is `P`, and the sum of the numbers with a `-` sign is `Q`. Thus, we have:
     - `P - Q = target`
     - `P + Q = sum(nums)`
   - By solving this system of equations, we can find that:
     - `P = (sum(nums) + target) / 2`
     - This means that we need to find the number of ways to select a subset of `nums` that adds up to `(sum(nums) + target) / 2`.

2. **Dynamic Programming**:
   - We can use dynamic programming to find the number of subsets that sum to a given value `P`. This is equivalent to the classic **Subset Sum Problem**.
   - We define `dp[i]` as the number of ways to get a sum of `i` using the elements in `nums`.

3. **Edge Case**:
   - If `sum(nums) + target` is odd or negative, it’s impossible to find such a subset, and the answer should be `0`.

### Solution Code:

```python
def findTargetSumWays(nums, target):
    total_sum = sum(nums)
    
    # If the total sum plus the target is odd or negative, no solution
    if (total_sum + target) % 2 != 0 or total_sum < target:
        return 0
    
    # Find the subset sum P that we need to target
    subset_sum = (total_sum + target) // 2
    
    # Initialize DP array to count number of ways to get each sum
    dp = [0] * (subset_sum + 1)
    dp[0] = 1  # There's one way to achieve a sum of 0: choose no elements
    
    # Update the DP array by considering each number in the nums array
    for num in nums:
        for i in range(subset_sum, num - 1, -1):
            dp[i] += dp[i - num]
    
    return dp[subset_sum]
```

## Explanation of the Code:

1. **Initial Checks**:
   - Calculate `total_sum`, the sum of all elements in `nums`. If the sum of `total_sum + target` is odd or if `total_sum` is less than the target, there is no solution, so return `0`.

2. **Subset Sum Calculation**:
   - Calculate the subset sum `P` using the formula `(total_sum + target) // 2`. This is the sum we need to find from a subset of `nums`.

3. **Dynamic Programming Array**:
   - We use an array `dp` where `dp[i]` represents the number of ways to achieve a sum of `i` using the elements from `nums`.
   - Initialize `dp[0] = 1` because there is exactly one way to achieve a sum of `0`—by choosing no elements.

4. **Updating the DP Array**:
   - For each number `num` in `nums`, we update the DP array in reverse order. This ensures that each number is only counted once for each possible sum.

5. **Return the Result**:
   - After processing all numbers, `dp[subset_sum]` contains the number of ways to achieve the sum `P`, which corresponds to the number of ways to assign `+` and `-` signs such that their sum equals the target.

## Time and Space Complexity:

- **Time Complexity**: O(n * subset_sum), where `n` is the length of the `nums` array and `subset_sum` is the target subset sum (i.e., `(total_sum + target) / 2`).
  - We iterate over all elements of `nums` and for each element, we update the DP array of size `subset_sum`.

- **Space Complexity**: O(subset_sum), as we only need an array `dp` of size `subset_sum + 1`.

## Example Walkthrough:

For `nums = [1, 1, 1, 1, 1]` and `target = 3`:

1. **Initial Calculations**:
   - `total_sum = 5`, `subset_sum = (5 + 3) // 2 = 4`.
   
2. **DP Initialization**:
   - `dp = [1, 0, 0, 0, 0]` (initial state with one way to get sum `0`).

3. **Processing Each Number**:
   - Process the first `1` in `nums`, update `dp[1]` and `dp[2]`, etc.
   - Repeat for the remaining numbers.

4. **Final DP State**:
   - After processing all numbers, `dp[4] = 5`, meaning there are 5 ways to assign `+` and `-` signs such that their sum equals 3.

Thus, the final result is `5`.

## Conclusion

This dynamic programming solution effectively transforms the problem into a subset sum problem, allowing us to compute the number of ways to achieve the target sum by partitioning the input list. The time and space complexities are efficient given the problem constraints.