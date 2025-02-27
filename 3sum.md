#python3sum #3sum #3sumpython
Approach used is 2pointers and we skip duplicate numbers in an array by incrementing left pointer and decrementing the right pointer.

Time complexity : O(n^2)
space complexity : O(1)


```python
def three_sum(nums):
    nums.sort()
    n = len(nums)
    result = []

    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        l, r = i + 1, n - 1
        while l < r:
            total = nums[i] + nums[l] + nums[r]
            if total == 0:
                result.append([nums[i], nums[l], nums[r]])

                while l < r and nums[l] == nums[l + 1]:
                    l += 1
                while l < r and nums[r] == nums[r - 1]:
                    r -= 1
                l += 1
                r -= 1
            elif total < 0:
                l += 1
            else:
                r -= 1

    return result


nums = [-1, 0, 2, 1, -1, -4]
print(three_sum(nums))
```
# Leetcode 3 sum smaller
#python3sumsmaller #3sumsmaller #3sumpythonsmaller #2pointer
Time complexity : O(n^2)
space complexity : O(1)
```python
    def threeSumSmaller(self, nums: List[int], target: int) -> int:
        nums.sort() # Sort the array
        count=0
        n=len(nums)
        for i in range(0,n-2):
            left,right=i+1,n-1
            while left<right: # Fix first element
                sum=nums[i]+nums[left]+nums[right]
                if sum<target:
                    count+=right-left # All pairs (left, left+1, ..., right) are valid
                    left+=1 # Move left pointer forward
                else:
                    right-=1 # Move right pointer backward
        return count
```



# Solution to "15. 3Sum"

## Problem Statement

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that:

- `i != j`, `i != k`, and `j != k`
- `nums[i] + nums[j] + nums[k] == 0`

The solution set must not contain duplicate triplets.

Example:

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2], [-1,0,1]]
```

---

## Approach: Two-Pointer Technique

### Explanation

1. **Sort the Array:** Sort `nums` to simplify duplicate detection and use the two-pointer approach.
2. **Iterate through the array:** For each element `nums[i]`, find two numbers `nums[left]` and `nums[right]` such that `nums[i] + nums[left] + nums[right] == 0`.
3. **Avoid Duplicates:** Skip duplicate values after finding a valid triplet.

---

## Implementation in Python

```python
def threeSum(nums):
    nums.sort()
    result = []

    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue  # Skip duplicate `i`

        left, right = i + 1, len(nums) - 1

        while left < right:
            total = nums[i] + nums[left] + nums[right]

            if total == 0:
                result.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1

                while left < right and nums[left] == nums[left - 1]:
                    left += 1  # Skip duplicate `left`
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1  # Skip duplicate `right`

            elif total < 0:
                left += 1
            else:
                right -= 1

    return result

# Example usage
# nums = [-1, 0, 1, 2, -1, -4]
# print(threeSum(nums))  # Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n^2)` where `n` is the number of elements in `nums`.
    - Sorting takes `O(n log n)` and the two-pointer search takes `O(n^2)`.
2. **Space Complexity:** `O(1)` (excluding the output list).

---

## Example Run

Input:

```
[-1, 0, 1, 2, -1, -4]
```

Output:

```
[[-1, -1, 2], [-1, 0, 1]]
```

---

## Edge Cases

1. No triplets: `nums = [1, 2, 3]` → Output: `[]`
2. All zeros: `nums = [0, 0, 0, 0]` → Output: `[[0, 0, 0]]`
3. Less than 3 elements: `nums = [1, 2]` → Output: `[]`

---

## Conclusion

This solution efficiently finds unique triplets that sum to zero using sorting and the two-pointer technique.