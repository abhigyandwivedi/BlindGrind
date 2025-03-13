# Solution to "169. Majority Element"

## Problem Statement

Given an array `nums` of size `n`, return the majority element. The majority element is the element that appears more than `n / 2` times. You may assume that the array is non-empty and the majority element always exists.

Example:

```
Input: nums = [3,2,3]
Output: 3
```

---

## Approach: Boyer-Moore Voting Algorithm

### Explanation

1. **Candidate Selection:** Use a counter to find the most frequent element.
2. **Candidate Verification:** Since the problem guarantees a majority element, we skip the verification step.

---

## Implementation in Python

```python
def majority_element(nums):
    count, candidate = 0, None

    for num in nums:
        if count == 0:
            candidate = num
        count += (1 if num == candidate else -1)

    return candidate
```

---

## Example Run

Input:

```python
nums = [3, 2, 3]
print(majority_element(nums))
```

Output:

```
3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - `N` is the length of `nums`.
    - Each element is processed once.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for counters.

---

## Edge Cases

1. Single element → Output: that element.
2. All identical elements → Output: that element.

---

## Conclusion

The Boyer-Moore Voting Algorithm ensures efficient majority detection in linear time with constant space.


**********************************
# Majority Element ii

```python
class Solution(object):
    def majority_element_ii(self, nums):
            """
            :type nums: List[int]
            :rtype: List[int]
            """
            n = len(nums)

            # Initialize two candidates and their counts
            ele1, ele2 = -1, -1
            cnt1, cnt2 = 0, 0

            for ele in nums:
                # Increment count for candidate 1
                if ele1 == ele:
                    cnt1 += 1
                # Increment count for candidate 2
                elif ele2 == ele:
                    cnt2 += 1
                # New candidate 1 if count is zero
                elif cnt1 == 0:
                    ele1 = ele
                    cnt1 += 1
                # New candidate 2 if count is zero
                elif cnt2 == 0:
                    ele2 = ele
                    cnt2 += 1
                # Decrease counts if neither candidate
                else:
                    cnt1 -= 1
                    cnt2 -= 1

            res = []
            cnt1, cnt2 = 0, 0

            # Count the occurrences of candidates
            for ele in nums:
                if ele1 == ele:
                    cnt1 += 1
                if ele2 == ele:
                    cnt2 += 1

            # Add to result if they are majority elements
            if cnt1 > n / 3:
                res.append(ele1)
            if cnt2 > n / 3 and ele1 != ele2:
                res.append(ele2)

            if len(res) == 2 and res[0] > res[1]:
                res[0], res[1] = res[1], res[0]

            return res
                    
```