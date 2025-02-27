# Solution to "217. Contains Duplicate"

## Problem Statement

Given an integer array `nums`, return `true` if any value appears at least twice in the array and `false` if every element is distinct.

Example:

```
Input: nums = [1,2,3,1]
Output: true
```

---

## Approach: Hash Set

### Explanation

1. **Use a Set:** Iterate through the array while storing elements in a set.
2. **Check for Duplicates:** If an element already exists in the set, return `true`.
3. **Return `false`:** If no duplicates are found after iteration, return `false`.

---

## Implementation in Python

```python
def containsDuplicate(nums):
    seen = set()
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    return False
```

---

## Example Run

Input:

```python
nums = [1, 2, 3, 1]
print(containsDuplicate(nums))
```

Output:

```
True
```

Explanation:

- The number `1` appears twice in the array.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each element is processed once.
2. **Space Complexity:** `O(n)`
    
    - Extra space for the set to store unique elements.

---

## Edge Cases

1. Empty array → `False`.
2. Array with one element → `False`.
3. All unique elements → `False`.
4. Multiple duplicates → `True`.

---

## Conclusion

Using a hash set allows for efficient detection of duplicates in linear time.