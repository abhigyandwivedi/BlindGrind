# Solution to "67. Add Binary"

## Problem Statement

Given two binary strings `a` and `b`, return their sum as a binary string.

Example:

```
Input: a = "1010", b = "1011"
Output: "10101"
```

---

## Approach: Bit-by-Bit Addition

### Explanation

1. **Reverse Strings:** Start from the least significant bit by reversing both strings.
2. **Bitwise Addition:** Add corresponding bits with a carry.
3. **Handle Carry:** If there's a carry left after the last addition, append it.
4. **Reverse Result:** Reverse the result to get the final binary string.

---

## Implementation in Python

```python
def addBinary(a: str, b: str) -> str:
    i, j, carry = len(a) - 1, len(b) - 1, 0
    result = []

    while i >= 0 or j >= 0 or carry:
        bit_a = int(a[i]) if i >= 0 else 0
        bit_b = int(b[j]) if j >= 0 else 0
        total = bit_a + bit_b + carry
        result.append(str(total % 2))
        carry = total // 2
        i -= 1
        j -= 1

    return ''.join(result[::-1])
```

---

## Example Run

Input:

```python
a = "1010"
b = "1011"
print(addBinary(a, b))
```

Output:

```
"10101"
```

---

## Complexity Analysis

1. **Time Complexity:** `O(max(N, M))`
    
    - `N` and `M` are the lengths of `a` and `b`.
    - Each bit is processed once.
2. **Space Complexity:** `O(max(N, M))`
    
    - The result stores the sum bit-by-bit.

---

## Edge Cases

1. `a = "0", b = "0"` → Output: `"0"`
2. Unequal lengths like `a = "1", b = "101"` → Output: `"110"`
3. Carry propagation like `a = "1111", b = "1"` → Output: `"10000"`

---

## Conclusion

The bit-by-bit addition approach ensures efficient binary summation by handling carries and edge cases effectively.