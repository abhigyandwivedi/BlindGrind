
# 673: Number of Longest Increasing Subsequence

## Problem Statement

Given an integer array `nums`, return the number of longest increasing subsequences (LIS). 

Notice that the sequence has to be strictly increasing.

### Example 1:
Input: `nums = [1,3,1,4,1,5]`  
Output: `2`  
Explanation: The longest increasing subsequences are `[1, 3, 4, 5]` and `[1, 3, 5]`.

### Example 2:
Input: `nums = [2,2,2,2,2]`  
Output: `5`  
Explanation: The longest increasing subsequences are `[2]`, `[2]`, `[2]`, `[2]`, and `[2]`.

### Constraints:
- 1 <= `nums.length` <= 2000
- -10^9 <= `nums[i]` <= 10^9

## Approach

### Dynamic Programming Approach

To solve this problem, we can use a dynamic programming (DP) approach, where we maintain two arrays:
- **`dp[i]`**: The length of the longest increasing subsequence that ends at index `i`.
- **`count[i]`**: The number of longest increasing subsequences that end at index `i`.

#### Key Ideas:
1. For each element `nums[i]`, we look at all previous elements `nums[j]` (where `j < i`).
2. If `nums[j] < nums[i]`, then `nums[i]` can extend the subsequences ending at `nums[j]`.
3. For each such valid `j`, we:
   - If `dp[j] + 1 > dp[i]`, we have found a longer subsequence ending at `i`, so we update `dp[i]` and reset `count[i]` to `count[j]`.
   - If `dp[j] + 1 == dp[i]`, we add `count[j]` to `count[i]`, since this means there is another LIS that ends at `i` with the same length.

### Steps:

1. Initialize `dp[i] = 1` and `count[i] = 1` for each element, as the minimum subsequence length for any element is 1 (itself).
2. For each element, compare it with all previous elements and update `dp` and `count` arrays according to the above rules.
3. The longest increasing subsequence length is the maximum value in the `dp` array.
4. Sum up the number of subsequences whose length equals the longest subsequence length from the `count` array.

### Solution Code

```python
def findNumberOfLIS(nums):
    if not nums:
        return 0
    
    n = len(nums)
    dp = [1] * n  # dp[i] will store the length of the LIS ending at index i
    count = [1] * n  # count[i] will store the number of LIS ending at index i
    
    for i in range(1, n):
        for j in range(i):
            if nums[i] > nums[j]:
                if dp[j] + 1 > dp[i]:
                    dp[i] = dp[j] + 1
                    count[i] = count[j]
                elif dp[j] + 1 == dp[i]:
                    count[i] += count[j]
    
    max_len = max(dp)
    result = sum(count[i] for i in range(n) if dp[i] == max_len)
    
    return result
```

## Explanation of the Code:

1. **Initial Setup**:
   - We initialize two arrays `dp` and `count` with the size of `n`. The value of `dp[i]` represents the length of the longest increasing subsequence that ends at index `i`. The value of `count[i]` represents how many longest increasing subsequences end at index `i`.
   
2. **Main Loop**:
   - The outer loop iterates through each element in the list `nums`, starting from index `1`.
   - The inner loop checks all previous elements (from `0` to `i-1`). For each pair `(i, j)` where `i > j`, we check if `nums[i] > nums[j]` (strictly increasing). 
   
3. **Updating `dp` and `count`**:
   - If `dp[j] + 1 > dp[i]`, it means we can extend the subsequence ending at `j` to `i`. Thus, we update `dp[i]` and set `count[i]` to `count[j]` (since the number of ways to extend the subsequence is the same as the number of ways to end it at `j`).
   - If `dp[j] + 1 == dp[i]`, it means we can extend another subsequence, so we add `count[j]` to `count[i]` (adding more ways to form the subsequence ending at `i`).

4. **Find the Maximum LIS Length**:
   - After processing all elements, the longest increasing subsequence length will be the maximum value in `dp`.
   
5. **Sum the Counts**:
   - Finally, we sum up all the counts where `dp[i]` equals the maximum length of the LIS to get the total number of LIS.

## Time Complexity:

- **Time Complexity**: O(n^2), where `n` is the length of the input list `nums`. This is because for each element, we compare it with all the previous elements in a nested loop.
- **Space Complexity**: O(n), because we use two arrays (`dp` and `count`), each of size `n`.

## Example Walkthrough

Consider the input `nums = [1, 3, 1, 4, 1, 5]`:

1. Initialize `dp = [1, 1, 1, 1, 1, 1]` and `count = [1, 1, 1, 1, 1, 1]`.
2. Iterating through each element:
   - For `i = 1`, compare with `j = 0`. Since `nums[1] > nums[0]`, we update `dp[1] = 2` and `count[1] = 1`.
   - For `i = 2`, compare with `j = 0`. Since `nums[2] > nums[0]`, we update `dp[2] = 2` and `count[2] = 1`.
   - For `i = 3`, compare with `j = 0`, `j = 1`, `j = 2`. Update `dp[3] = 3` and `count[3] = 2` (two ways to form subsequences of length 3).
   - For `i = 4`, compare with `j = 0`, `j = 1`, `j = 2`, `j = 3`. Update `dp[4] = 3` and `count[4] = 2`.
   - For `i = 5`, compare with `j = 0`, `j = 1`, `j = 2`, `j = 3`, `j = 4`. Update `dp[5] = 4` and `count[5] = 2` (two ways to form subsequences of length 4).

3. The longest increasing subsequence length is `max(dp) = 4`, and the number of LIS is the sum of `count[i]` where `dp[i] == 4`, which is `2`.

Thus, the result is `2`.

## Conclusion

This dynamic programming approach efficiently computes the number of longest increasing subsequences. The time complexity is O(n^2), which is manageable for inputs up to 2000 elements. The space complexity is O(n) due to the use of two arrays for `dp` and `count`.