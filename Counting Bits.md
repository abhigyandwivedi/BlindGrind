# Solution to "338. Counting Bits"

## Problem Statement

Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (`0 <= i <= n`), `ans[i]` is the number of `1`s in the binary representation of `i`.

---

## Approach: Dynamic Programming

### Explanation

We use a dynamic programming approach with the following observation:

- For any number `i`, the number of `1` bits is `ans[i >> 1] + (i & 1)`.
    - `i >> 1` shifts `i` to the right by 1 bit, effectively dividing by 2.
    - `(i & 1)` checks if the last bit is `1` (odd number).

### Algorithm Steps

1. Initialize an array `ans` of size `n + 1` with all zeros.
2. Iterate through `i` from `1` to `n`.
3. For each `i`, compute `ans[i] = ans[i >> 1] + (i & 1)`.
4. Return the `ans` array.

---

## Implementation in Python

```python
class Solution:
    def countBits(self, n: int) -> list[int]:
        ans = [0] * (n + 1)
        for i in range(1, n + 1):
            ans[i] = ans[i >> 1] + (i & 1)
        return ans
```

---

## Example Run

Input:

```python
n = 5
solution = Solution()
print(solution.countBits(n))
```

Output:

```
[0, 1, 1, 2, 1, 2]
```

Explanation:

- `0` → `0` → `0` ones
- `1` → `1` → `1` one
- `2` → `10` → `1` one
- `3` → `11` → `2` ones
- `4` → `100` → `1` one
- `5` → `101` → `2` ones

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each number from `0` to `n` is processed once.
2. **Space Complexity:** `O(n)`
    
    - The `ans` array stores the count of `1`s for each number.

---

## Edge Cases

1. `n = 0` → Output: `[0]`
2. `n = 1` → Output: `[0, 1]`

---

## Conclusion

This solution efficiently counts the number of `1`s in binary representation for numbers from `0` to `n` using a dynamic programming approach.