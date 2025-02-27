# Solution to "70. Climbing Stairs"

## Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top. Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Example:

```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top:
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

---

## Approach: Dynamic Programming (Fibonacci Sequence)

### Explanation

1. This problem follows the Fibonacci pattern.
2. Let `dp[i]` represent the number of ways to reach step `i`.
3. The recurrence relation is:
    
    ```
    dp[i] = dp[i - 1] + dp[i - 2]
    ```
    
    This is because you can reach step `i` either from step `i-1` (1 step) or step `i-2` (2 steps).
4. Base cases:
    - `dp[0] = 1` (One way to stay at the ground level.)
    - `dp[1] = 1` (One way to take the first step.)

---

## Implementation in Python

```python
def climbStairs(n: int) -> int:
    if n <= 1:
        return 1

    first, second = 1, 1

    for i in range(2, n + 1):
        first, second = second, first + second

    return second

# Example usage
n = 3
print(climbStairs(n))  # Output: 3
```

---

## Example Run

Input:

```python
n = 5
print(climbStairs(n))  # Output: 8
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - We iterate from `2` to `n`.
2. **Space Complexity:** `O(1)` - We use constant space to store only two variables.

---

## Edge Cases

1. `n = 0`: Output → `1` (No steps to climb.)
2. `n = 1`: Output → `1` (Only one way.)
3. `n = 2`: Output → `2` (1+1 or 2.)

---

## Conclusion

This solution efficiently computes the number of ways to climb stairs using a Fibonacci-like dynamic programming approach with constant space.