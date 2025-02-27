# Solution to "528. Random Pick with Weight"

## Problem Statement

You are given an array `w` where `w[i]` represents the weight of the `i`th index. Write a function `pickIndex()` that picks an index randomly according to its weight.

For example, given `w = [1, 3, 2]`, the probability of picking index `0` is `1/6`, index `1` is `3/6`, and index `2` is `2/6`.

---

## Approach: Prefix Sum with Binary Search

### Explanation

We can solve this problem using the prefix sum array and binary search.

### Algorithm Steps

1. **Prefix Sum Array:**
    
    - Create a prefix sum array where each element represents the cumulative sum up to that index.
    - For `w = [1, 3, 2]`, the prefix sum becomes `[1, 4, 6]`.
2. **Random Pick:**
    
    - Generate a random number `x` between `1` and the total sum of weights (`6` in this case).
    - Use binary search to find the first index where the prefix sum is greater than or equal to `x`.

### Example Walkthrough

For example, given the weights:

```
w = [1, 3, 2]
```

1. Prefix sum array:

```
[1, 4, 6]
```

1. If the random number `x` is:
    - `1`: Pick index `0`
    - `2`, `3`, `4`: Pick index `1`
    - `5`, `6`: Pick index `2`

---

## Implementation in Python

```python
import random
import bisect

class Solution:
    def __init__(self, w: List[int]):
        self.prefix_sums = []
        self.total_sum = 0

        for weight in w:
            self.total_sum += weight
            self.prefix_sums.append(self.total_sum)

    def pickIndex(self) -> int:
        target = random.randint(1, self.total_sum)
        return bisect.bisect_left(self.prefix_sums, target)
```

---

## Example Run

Input:

```python
w = [1, 3, 2]
solution = Solution(w)
print(solution.pickIndex())
```

Output (example runs):

```
1
2
1
```

---

## Complexity Analysis

1. **Time Complexity:**
    
    - Initialization: `O(n)` to build the prefix sum array.
    - Pick Index: `O(log n)` using binary search.
2. **Space Complexity:** `O(n)`
    
    - Extra space used for the prefix sum array.

---

## Edge Cases

1. Single weight → Always return index `0`.
2. All weights equal → Each index has equal probability.

---

## Conclusion

This solution efficiently picks an index based on weights using the prefix sum array and binary search, achieving logarithmic time complexity for each pick operation.