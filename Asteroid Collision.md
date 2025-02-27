# Solution to "735. Asteroid Collision"

## Problem Statement

You are given an array `asteroids` representing asteroids in a row. For each asteroid, the absolute value represents its size, and the sign represents its direction:

- Positive: Moving right
- Negative: Moving left

Asteroids move at the same speed. If two asteroids collide, the smaller one explodes. If they are the same size, both explode. Return the state of the asteroids after all collisions.

---

## Approach: Stack Simulation

### Explanation

We can efficiently solve this problem using a stack.

### Algorithm Steps

1. **Iterate through Asteroids:**
    
    - Push positive asteroids into the stack.
    - When encountering a negative asteroid, compare it with the top of the stack (right-moving asteroid).
2. **Collision Handling:**
    
    - If the top of the stack is smaller, pop the stack (right-moving asteroid explodes).
    - If the top is larger, the current left-moving asteroid explodes.
    - If equal, both explode.
3. **Add Remaining Asteroids:**
    
    - If no collision occurs, push the negative asteroid into the stack.

### Example Walkthrough

For example, given the input:

```
asteroids = [5, 10, -5]
```

1. `5` → Push into stack: `[5]`
2. `10` → Push into stack: `[5, 10]`
3. `-5` → Collides with `10` but explodes (as `10 > 5`). Stack remains `[5, 10]`.

Output:

```
[5, 10]
```

---

## Implementation in Python

```python
class Solution:
    def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []

        for asteroid in asteroids:
            while stack and asteroid < 0 and stack[-1] > 0:
                if abs(asteroid) > stack[-1]:
                    stack.pop()
                    continue
                elif abs(asteroid) == stack[-1]:
                    stack.pop()
                break
            else:
                stack.append(asteroid)

        return stack
```

---

## Example Run

Input:

```python
asteroids = [5, 10, -5]
solution = Solution()
print(solution.asteroidCollision(asteroids))
```

Output:

```
[5, 10]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each asteroid is pushed and popped from the stack once.
2. **Space Complexity:** `O(n)`
    
    - In the worst case, all asteroids are stored in the stack.

---

## Edge Cases

1. All positive asteroids → Return the same array.
2. All negative asteroids → Return the same array.
3. Multiple collisions → Properly resolve and return remaining asteroids.

---

## Conclusion

This solution efficiently simulates asteroid collisions using a stack, ensuring optimal time complexity of `O(n)` while handling all edge cases.