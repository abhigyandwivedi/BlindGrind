# 🧮 Basic Calculator II (LeetCode 227)

## 🚀 Problem Statement

Given a string `s` representing a basic mathematical expression with non-negative integers and the operators `+`, `-`, `*`, and `/`, evaluate the expression. The division should truncate towards zero.

### 🔑 Example:

```python
Input: s = "3+2*2"
Output: 7
Explanation: First, multiply 2 * 2 = 4, then add 3 + 4 = 7.
```

---

## 📝 **Optimized O(n) Solution: Stack-Based Approach**

```python
class Solution:
    def calculate(self, s: str) -> int:
        s = s.replace(" ", "")  # Remove spaces
        stack = []
        num = 0
        sign = '+'

        for i, char in enumerate(s):
            if char.isdigit():
                num = num * 10 + int(char)

            if char in '+-*/' or i == len(s) - 1:
                if sign == '+':
                    stack.append(num)
                elif sign == '-':
                    stack.append(-num)
                elif sign == '*':
                    stack.append(stack.pop() * num)
                elif sign == '/':
                    stack.append(int(stack.pop() / num))  # Truncate towards zero

                sign = char
                num = 0

        return sum(stack)

# Example usage
s = "3+2*2"
solution = Solution()
print(solution.calculate(s))  # Output: 7
```

---

## ⏱️ **Time Complexity Analysis**

1. **Single Pass:** The string is traversed once, processing each character.
2. **Stack Operations:** Push, pop, and arithmetic operations are all O(1)O(1).

Thus, the overall time complexity is:

O(n)O(n)

Where `n` is the length of the input string.

---

## 💾 **Space Complexity Analysis**

- **Stack Storage:** The stack stores intermediate results.
- **Worst-case Stack Size:** In case of only addition or subtraction, the stack can hold `n/2` elements.

Thus, the overall space complexity is:

O(n)O(n)

---

## ✅ **Key Insights:**

1. Process numbers and operators sequentially.
2. Use a stack to handle precedence without parentheses.
3. Multiply and divide immediately, push results to the stack.
4. Sum up the stack for the final result.
5. O(n)O(n) time and O(n)O(n) space ensure efficiency for large inputs.