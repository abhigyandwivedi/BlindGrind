# 🟢 First Missing Positive - LeetCode Solution (Python)

## 🚀 **Problem Statement**

Given an unsorted integer array `nums`, find the smallest missing positive integer.

**Example:**

```python
Input: nums = [3, 4, -1, 1]
Output: 2
```

---

## 🟡 **Solution Explanation (Cyclic Sort Approach)**

1. **Key Insight:**
    
    - The first missing positive must be between `1` and `n+1` (where `n` is the array length).
    - Place each number `nums[i]` at its correct index `nums[i] - 1` if valid (`1` to `n`).
2. **Approach:**
    
    - Swap elements to their correct positions using cyclic sort.
    - Find the first index `i` where `nums[i] != i + 1`.
3. **Complexity:**
    
    - 🕰️ **Time:** O(n)O(n), each element is moved once.
    - 💾 **Space:** O(1)O(1), in-place sorting.

---

## 📝 **Python Code Implementation**

```python
def first_missing_positive(nums):
    n = len(nums)
    
    # Step 1: Place each number in its correct position
    for i in range(n):
        while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
            nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]  # Swap

    # Step 2: Find the first missing positive
    for i in range(n):
        if nums[i] != i + 1:
            return i + 1

    # If all are in place, return n + 1
    return n + 1

# Example usage
nums = [3, 4, -1, 1]
result = first_missing_positive(nums)
print(f"The first missing positive integer is: {result}")
```

---

## ✅ **Example Run:**

For `nums = [3, 4, -1, 1]`, the output is:

```
The first missing positive integer is: 2
```

**Explanation:**

- After sorting: `[-1, 1, 3, 4] → [1, -1, 3, 4] → [1, 3, -1, 4] → [1, -1, 3, 4]`
- Missing positive is `2`.

---

## ⚙️ **Edge Cases:**

1. `[]` → Output: `1`
2. `[1, 2, 0]` → Output: `3`
3. `[7, 8, 9, 11, 12]` → Output: `1`

---

# 🟢 First Missing Positive - LeetCode Solution (Python)

## 🚀 **Problem Statement**

Given an unsorted integer array `nums`, find the smallest missing positive integer.

**Example:**

```python
Input: nums = [3, 4, -1, 1]
Output: 2
```

---

## 🟡 **Solution Explanation (Hash Table Approach)**

1. **Key Insight:**
    
    - Use a hash set to store all positive integers from the array.
    - Iterate from `1` to `n+1` and find the first integer not in the set.
2. **Approach:**
    
    - Add all positive integers to a set.
    - Check each number from `1` onward to find the missing one.
3. **Complexity:**
    
    - 🕰️ **Time:** O(n), each element is processed once.
    - 💾 **Space:** O(n), due to the hash set.

---

## 📝 **Python Code Implementation**

```python
def first_missing_positive(nums):
    num_set = set(nums)
    
    # Find the first missing positive
    for i in range(1, len(nums) + 2):
        if i not in num_set:
            return i

# Example usage
nums = [3, 4, -1, 1]
result = first_missing_positive(nums)
print(f"The first missing positive integer is: {result}")
```

---

## ✅ **Example Run:**

For `nums = [3, 4, -1, 1]`, the output is:

```
The first missing positive integer is: 2
```

**Explanation:**

- Positive integers present: `{1, 3, 4}`
- Missing positive is `2`.

---

## ⚙️ **Edge Cases:**

1. `[]` → Output: `1`
2. `[1, 2, 0]` → Output: `3`
3. `[7, 8, 9, 11, 12]` → Output: `1`

---
