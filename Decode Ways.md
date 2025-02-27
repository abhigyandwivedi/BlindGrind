# LeetCode 91: Decode Ways

## Problem Statement

A message containing letters from `A` to `Z` can be encoded into numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a string `s` containing only digits, return the number of ways to decode it.

### Example Input

```
Input: s = "226"
```

### Example Output

```
Output: 3
```

### Explanation

The possible decodings are:

1. "2" + "2" + "6" -> "BBF"
2. "22" + "6" -> "VF"
3. "2" + "26" -> "BZ"

---

## Approach

We can solve this problem using **Dynamic Programming (DP)**.

### Steps:

1. Define a DP array `dp` where `dp[i]` represents the number of ways to decode the string up to index `i-1`.
2. Initialize `dp[0] = 1` (empty string has one way to decode).
3. Iterate through the string and check:
    - If the current digit (`s[i-1]`) is valid (1 to 9), add `dp[i-1]`.
    - If the two-digit number (`s[i-2]s[i-1]`) is between 10 and 26, add `dp[i-2]`.
4. `dp[n]` will hold the final count.

---

## Solution (Python)

```python
def numDecodings(s: str) -> int:
    if not s or s[0] == '0':
        return 0

    n = len(s)
    dp = [0] * (n + 1)
    dp[0] = 1  # Base case: one way to decode an empty string

    for i in range(1, n + 1):
        # Single-digit decode
        if s[i - 1] != '0':
            dp[i] += dp[i - 1]

        # Two-digit decode
        if i > 1 and 10 <= int(s[i - 2:i]) <= 26:
            dp[i] += dp[i - 2]

    return dp[n]

# Example usage
s = "226"
print(numDecodings(s))  # Output: 3
```

---

## Detailed Explanation

1. **Initialization:**
    
    - `dp[0] = 1`: One way to decode an empty string.
    - `dp[i]` represents ways to decode the first `i` characters.
2. **Single-digit check:**
    
    - If `s[i-1]` is not `'0'`, it can be decoded alone, so `dp[i] += dp[i-1]`.
3. **Two-digit check:**
    
    - If `10 <= int(s[i-2:i]) <= 26`, decode as a pair, so `dp[i] += dp[i-2]`.
4. **Example Run (s = "226"):**
    
    - `dp[0] = 1`
    - `dp[1] = 1` ("2")
    - `dp[2] = 2` ("22" or "2,2")
    - `dp[3] = 3` ("226", "2,26", "22,6")

---

## Complexity Analysis

### Time Complexity: O(N)

- **Explanation:** We iterate through the string once, checking one- and two-digit combinations.

### Space Complexity: O(N)

- **Explanation:** The `dp` array stores results for each index up to `n`.

---

## Edge Cases

1. `s = "0"` → Output: `0` (no valid decoding)
2. `s = "10"` → Output: `1` ("J")
3. `s = "101"` → Output: `1` ("JA")
4. `s = "11106"` → Output: `2` ("AAJF" and "KJF")

---

## Conclusion

This solution efficiently computes the number of ways to decode a string using dynamic programming, ensuring optimal time and space complexity.

---

Let me know if you'd like further clarifications or optimizations!