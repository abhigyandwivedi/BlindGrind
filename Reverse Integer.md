# Reverse Integer Solution

## Problem Statement

Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, return `0`.

### Example 1:

```
Input: x = 123
Output: 321
```

### Example 2:

```
Input: x = -123
Output: -321
```

### Example 3:

```
Input: x = 120
Output: 21
```

### Example 4:

```
Input: x = 0
Output: 0
```

---

## Approach: Mathematical Method

### Explanation

1. **Extract Digits:**
    
    - Get the last digit using `x % 10`.
    - Remove the last digit using integer division `x // 10`.
2. **Build the Reversed Number:**
    
    - Multiply the result by `10` and add the extracted digit.
3. **Handle Overflow:**
    
    - Check if the result exceeds the signed 32-bit range `[-2^31, 2^31 - 1]`.
4. **Return:**
    
    - If overflow occurs, return `0`; otherwise, return the reversed integer.

---

## Implementation in Python

```python
class Solution:
    def reverse(self, x: int) -> int:
        INT_MAX = 2**31 - 1  # 2147483647
        INT_MIN = -2**31     # -2147483648
        
        result = 0
        sign = 1 if x > 0 else -1
        x = abs(x)
        
        while x != 0:
            digit = x % 10
            x //= 10
            
            # Check for overflow before adding the digit
            if result > (INT_MAX - digit) // 10:
                return 0
            
            result = result * 10 + digit
        
        return sign * result
```

---

## Dry Run Example

For `x = -123`:

1. `digit = 3`, `result = 0 * 10 + 3 = 3`, `x = 12`
2. `digit = 2`, `result = 3 * 10 + 2 = 32`, `x = 1`
3. `digit = 1`, `result = 32 * 10 + 1 = 321`, `x = 0`
4. Return `-321`.

---

## Complexity Analysis

### Time Complexity

- **O(log10(x))**: The number of iterations depends on the number of digits in `x`. For a number with `d` digits, there will be `d` iterations.

### Space Complexity

- **O(1)**: Only a few variables are used for intermediate calculations.

---

## Edge Cases

1. `x = 0` → Output: `0`
2. `x = 1534236469` → Output: `0` (due to overflow)
3. `x = -2147483412` → Output: `-2143847412`

---

## Conclusion

This solution efficiently reverses an integer while handling potential overflows by checking conditions before updating the result.