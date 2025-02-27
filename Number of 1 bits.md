# Solution to "191. Number of 1 Bits"

## Problem Statement

Given an unsigned integer, return the number of '1' bits it has (also known as the Hamming weight).

---

## Approach: Bit Manipulation

### Explanation

We iterate through the bits of the integer and count the number of `1` bits using bitwise operations.

### Algorithm Steps

1. **Initialize:** Set `count = 0`.
2. **Iterate:** While `n > 0`, check the least significant bit using `n & 1`.
3. **Count:** If the bit is `1`, increment `count`.
4. **Shift:** Right shift `n` by one position (`n >>= 1`).
5. **Return:** After traversal, return `count`.

---

## Implementation in Python

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0
        while n:
            count += n & 1
            n >>= 1
        return count
```

---

## Example Run

Input:

```python
n = 11  # Binary: 1011
solution = Solution()
print(solution.hammingWeight(n))
```

Output:

```
3
```

---

## Complexity Analysis

1. **Time Complexity:** `O(1)`
    
    - The maximum number of iterations is `32` for a 32-bit integer.
2. **Space Complexity:** `O(1)`
    
    - Constant space used for variables.

---

## Edge Cases

1. `n = 0` → Output: `0`.
2. `n = 1` → Output: `1`.
3. Maximum integer → Proper count of `1` bits.

---

## Conclusion

This solution efficiently counts the number of `1` bits using bitwise operations with optimal time complexity.