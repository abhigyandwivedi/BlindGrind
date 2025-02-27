# LeetCode 268: Missing Number

## Problem Statement

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

### Example Input

```
Input: nums = [3, 0, 1]
```

### Example Output

```
Output: 2
```

### Explanation

The range `[0, 3]` includes the numbers `0`, `1`, `2`, and `3`. The missing number is `2`.

---

## Approach

We can solve this problem using several approaches:

### 1. **Mathematical Approach (Sum Formula)**

- Calculate the expected sum of numbers from `0` to `n` using the formula:
    
    expected_sum=n×(n+1)2\text{expected\_sum} = \frac{n \times (n + 1)}{2}
- Find the actual sum of elements in the array.
    
- The missing number is the difference between the expected sum and the actual sum.
    

---

## Solution (Python)

```python
def missingNumber(nums):
    n = len(nums)
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(nums)
    return expected_sum - actual_sum

# Example usage
nums = [3, 0, 1]
print(missingNumber(nums))  # Output: 2
```

---

## Detailed Explanation

1. **Input:** `nums = [3, 0, 1]`
2. **Length of Array:** `n = 3`
3. **Expected Sum:** `3 * (3 + 1) / 2 = 6`
4. **Actual Sum:** `3 + 0 + 1 = 4`
5. **Missing Number:** `6 - 4 = 2`

---

## Complexity Analysis

### Time Complexity: O(N)

- **Explanation:** We iterate through the array once to compute the sum, leading to `O(N)` complexity.

### Space Complexity: O(1)

- **Explanation:** Only constant extra space is used for variables.

---

## Alternative Approaches

1. **Bit Manipulation:**
    
    - XOR all indices and numbers. The remaining value will be the missing number.
    - Time Complexity: `O(N)`, Space Complexity: `O(1)`.
2. **Sorting:**
    
    - Sort the array and find the missing number by checking indices.
    - Time Complexity: `O(N log N)`, Space Complexity: `O(1)`.

---

## Edge Cases

1. `nums = [0]` → Output: `1` (missing number in range `[0, 1]`).
2. `nums = [1, 2]` → Output: `0` (missing number at the start).
3. `nums = [0, 1, 2, 3, 4]` → Output: `5` (missing last number).

---

## Conclusion

The mathematical approach provides an optimal solution with linear time complexity and constant space, making it efficient for large inputs.

---

Let me know if you'd like further clarifications or alternative solutions!

**Missing number xor soln
```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        xor1=0
        xor2=0
        n=len(nums)
        for i in nums:
            xor2^=i

        for i in range (1,n+1):
            xor1^=i

        return xor1^xor2
```