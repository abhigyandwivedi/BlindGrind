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
def majorityElement(nums):
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
print(majorityElement(nums))
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