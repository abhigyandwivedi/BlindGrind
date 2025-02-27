# Solution to "50. Pow(x, n)"

## Problem Statement

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

Given two numbers:

- `x` (a floating-point number)
- `n` (an integer)

Return the result of `x` raised to the power of `n`.

---

## Approach: Efficient Exponentiation (Binary Exponentiation)

### Explanation

We use **Binary Exponentiation** to efficiently compute the power. The key idea is to reduce the number of multiplications by splitting the problem into smaller subproblems:

1. **Base Case:**
    
    - If `n == 0`, return `1` (any number raised to the power of 0 is 1).
2. **Recursive Approach:**
    
    - If `n` is even:
        - `x^n = (x^(n/2)) * (x^(n/2))`
    - If `n` is odd:
        - `x^n = x * (x^(n//2)) * (x^(n//2))`
3. **Handle Negative Powers:**
    
    - If `n` is negative, compute `1 / (x^-n)`.

By halving `n` at each step, we achieve logarithmic complexity.

---

## Implementation in Python

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        def power(x, n):
            if n == 0:
                return 1
            half = power(x, n // 2)
            if n % 2 == 0:
                return half * half
            else:
                return half * half * x

        if n < 0:
            x = 1 / x
            n = -n

        return power(x, n)
```

---

## Example Run

Input:

```python
x = 2.0
n = 10

solution = Solution()
print(solution.myPow(x, n))
```

Output:

```
1024.0
```

---

## Complexity Analysis

1. **Time Complexity:** `O(log n)`
    
    - At each step, we divide `n` by 2, leading to logarithmic recursion depth.
2. **Space Complexity:** `O(log n)`
    
    - Recursive call stack depth is proportional to `log n`.

---

## Edge Cases

1. `x = 0` and `n > 0`: Return `0`.
2. `x = any` and `n = 0`: Return `1`.
3. `x = any` and `n < 0`: Return `1 / (x^-n)`.
4. `x = 1` and `n = any`: Return `1`.

---

## Conclusion

Using binary exponentiation, we efficiently calculate the power in logarithmic time, ensuring optimal performance for large inputs.