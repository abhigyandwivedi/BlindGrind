# 271. Encode and Decode Strings

## Problem Statement

Design an algorithm to encode a list of strings into a single string and decode that string back into the original list of strings.

### Example

**Input:**

```
strings = ["hello", "world"]
```

**Output:**

```
Encoded: "5#hello5#world"
Decoded: ["hello", "world"]
```

**Explanation:** Each string is prefixed with its length followed by a delimiter (`#`).

---

## Approach: Length-Prefix Encoding

### Idea

1. **Encoding:**
    
    - For each string, prepend its length followed by a special delimiter (`#`).
    - Concatenate all encoded strings into a single string.
2. **Decoding:**
    
    - Read the length prefix until the `#` delimiter.
    - Extract the corresponding substring and continue until the end.

---

## Implementation (Python)

```python
class Codec:
    def encode(self, strs):
        """Encodes a list of strings to a single string."""
        return ''.join(f"{len(s)}#{s}" for s in strs)

    def decode(self, s):
        """Decodes a single string to a list of strings."""
        i, result = 0, []
        while i < len(s):
            j = s.find('#', i)
            length = int(s[i:j])
            i = j + 1
            result.append(s[i:i+length])
            i += length
        return result
```

---

## Example Run

For `strings = ["hello", "world"]`:

1. **Encoding:**

```
"hello" → "5#hello"
"world" → "5#world"
Encoded result: "5#hello5#world"
```

1. **Decoding:**

```
"5#hello5#world" → ["hello", "world"]
```

Output: `['hello', 'world']`

---

## Complexity Analysis

### Time Complexity

- **Encoding:** `O(n)` where `n` is the total length of all strings.
- **Decoding:** `O(n)` where `n` is the length of the encoded string.

### Space Complexity

- **Encoding:** `O(1)` additional space, output string takes `O(n)`.
- **Decoding:** `O(n)` to store the decoded strings.

---

## Edge Cases

1. Empty list → Encoded as an empty string: `""`.
2. Strings with `#` → Handled via length prefix.
3. Empty string in list → Encoded as `"0#"`.

---

## Conclusion

This solution efficiently encodes and decodes strings using length-prefix encoding, ensuring correctness while maintaining linear complexity for both operations.