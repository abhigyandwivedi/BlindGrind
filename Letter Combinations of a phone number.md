# Solution to "17. Letter Combinations of a Phone Number"

## Problem Statement

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

Example:

```
Input: digits = "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

---

## Approach: Backtracking

### Explanation

1. **Mapping:** Use a dictionary to map digits to corresponding letters, like a phone keypad.
2. **Recursive Backtracking:** For each digit, explore all possible letters and recursively build combinations.
3. **Base Case:** When the current path reaches the length of the input digits, add it to the result.

---

## Implementation in Python

```python
def letterCombinations(digits):
    if not digits:
        return []

    phone_map = {
        "2": "abc",
        "3": "def",
        "4": "ghi",
        "5": "jkl",
        "6": "mno",
        "7": "pqrs",
        "8": "tuv",
        "9": "wxyz"
    }

    result = []

    def backtrack(index, path):
        if index == len(digits):
            result.append("".join(path))
            return

        possible_letters = phone_map[digits[index]]
        for letter in possible_letters:
            path.append(letter)
            backtrack(index + 1, path)
            path.pop()

    backtrack(0, [])
    return result
```

---

## Example Run

Input:

```python
digits = "23"
print(letterCombinations(digits))
```

Output:

```
['ad', 'ae', 'af', 'bd', 'be', 'bf', 'cd', 'ce', 'cf']
```

Explanation:

- Each digit maps to corresponding letters, and combinations are formed recursively.

---

## Complexity Analysis

1. **Time Complexity:** `O(3^m * 4^n)`
    
    - `m` is the number of digits mapping to 3 letters (`2`, `3`, `4`, `5`, `6`, `8`).
    - `n` is the number of digits mapping to 4 letters (`7`, `9`).
2. **Space Complexity:** `O(m + n)`
    
    - Due to recursive call stack and result storage.

---

## Edge Cases

1. If `digits` is empty, return `[]`.
2. Single-digit input returns corresponding letters.

---

## Conclusion

This backtracking solution efficiently generates all letter combinations for given digits using recursion.