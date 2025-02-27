# 190. Reverse Bits

## Problem Statement

Reverse bits of a given 32-bit unsigned integer.

### Example

**Input:**

```
n = 00000010100101000001111010011100
```

**Output:**

```
964176192 (00111001011110000010100101000000)
```

**Explanation:** The input binary string `00000010100101000001111010011100` gets reversed to `00111001011110000010100101000000`, which corresponds to the unsigned integer `964176192`.

---

## Approach: Bit Manipulation

We can reverse the bits by iterating through each bit of the given integer. For each bit:

1. Extract the least significant bit (LSB).
2. Shift the result left by one position to make room for the new bit.
3. Append the extracted bit to the result.
4. Right shift the input integer to move to the next bit.

### Steps

1. Initialize `result` to `0`.
2. Iterate `32` times (as it's a 32-bit integer).
3. Extract the LSB using `n & 1`.
4. Left shift `result` by 1 and append the extracted bit.
5. Right shift `n` by 1.
6. Return `result` after all bits are processed.

---

## Implementation (Python)

```python
def reverseBits(n: int) -> int:
    result = 0
    for i in range(32):
        # Extract the least significant bit
        bit = n & 1
        # Shift result to the left and append the bit
        result = (result << 1) | bit
        # Right shift n to process the next bit
        n >>= 1
    return result
```

---

## Example Run

For `n = 43261596` (binary `00000010100101000001111010011100`):

- After reversing, we get `964176192` (binary `00111001011110000010100101000000`).

---

## Complexity Analysis

### Time Complexity

- **O(1):** We iterate exactly 32 times, independent of the input value.

### Space Complexity

- **O(1):** Only a few variables (`result` and `bit`) are used for computation.

---

## Edge Cases

1. `n = 0` → Output: `0` (all bits are zero).
2. `n = 4294967295` (`0xFFFFFFFF`) → Output: `4294967295` (all bits are one).

---

## Conclusion

This solution efficiently reverses the bits of a 32-bit unsigned integer using bitwise operations. The approach ensures constant time and space complexity, making it optimal for this task.