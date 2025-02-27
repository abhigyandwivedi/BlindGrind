# 🟢 Largest Number - LeetCode Solution (Python)

## 🚀 **Problem Statement**

Given a list of non-negative integers `nums`, arrange them such that they form the largest possible number.

**Example:**

```python
Input: nums = [10, 2]
Output: "210"
```

---

## 🟡 **Solution Explanation (Custom Sort Approach)**

1. **Key Insight:**
    
    - To form the largest number, concatenate numbers in the order that maximizes the result.
    - Compare numbers `x` and `y` by checking if `x+y > y+x` when treated as strings.
2. **Approach:**
    
    - Convert integers to strings.
    - Sort using a custom comparator: if `x+y > y+x`, place `x` before `y`.
    - Join sorted strings and handle edge cases like leading zeros.
3. **Complexity:**
    
    - 🕰️ **Time:** O(nlog⁡n), due to sorting.
    - 💾 **Space:** O(n), for storing string representations.

---

## 📝 **Python Code Implementation**

```python
from functools import cmp_to_key

def largest_number(nums):
    # Custom comparator for sorting
    def compare(x, y):
        if x + y > y + x:
            return -1
        elif x + y < y + x:
            return 1
        else:
            return 0

    # Convert numbers to strings and sort
    nums_str = sorted(map(str, nums), key=cmp_to_key(compare))

    # Join the sorted array into the largest number
    result = ''.join(nums_str)

    # Handle the edge case where the result is all zeros
    return '0' if result[0] == '0' else result

# Example usage
nums = [10, 2]
result = largest_number(nums)
print(f"The largest number is: {result}")
```

---

## ✅ **Example Run:**

For `nums = [10, 2]`, the output is:

```
The largest number is: 210
```

**Explanation:**

- Possible combinations: `10 + 2 = "102"`, `2 + 10 = "210"`
- The largest concatenation is `"210"`.

---

## ⚙️ **Edge Cases:**

1. `[0, 0]` → Output: `"0"`
2. `[3, 30, 34, 5, 9]` → Output: `"9534330"`
3. `[1]` → Output: `"1"`

---
