# Solution to "981. Time Based Key-Value Store"

## Problem Statement

Design a time-based key-value data structure that can store multiple values for the same key at different timestamps and retrieve the value based on a given timestamp.

Implement the `TimeMap` class:

1. `set(String key, String value, int timestamp)` – Stores the key with the given value and timestamp.
2. `get(String key, int timestamp)` – Returns the value at the given timestamp or the closest earlier one if it exists; otherwise, returns an empty string.

Example:

```
Input:
TimeMap timeMap = new TimeMap();
timeMap.set("foo", "bar", 1);
print(timeMap.get("foo", 1));  # Output: "bar"
print(timeMap.get("foo", 3));  # Output: "bar"
timeMap.set("foo", "bar2", 4);
print(timeMap.get("foo", 4));  # Output: "bar2"
print(timeMap.get("foo", 5));  # Output: "bar2"
```

---

## Approach: Hash Map + Binary Search

### Explanation

1. **Data Storage:** Use a hash map where each key maps to a list of `(timestamp, value)` pairs.
2. **Set Operation:** Append the `(timestamp, value)` pair to the list corresponding to the key.
3. **Get Operation:** Use binary search to find the closest timestamp less than or equal to the given timestamp.

---

## Implementation in Python

```python
from collections import defaultdict
import bisect

class TimeMap:
    def __init__(self):
        self.store = defaultdict(list)

    def set(self, key: str, value: str, timestamp: int) -> None:
        self.store[key].append((timestamp, value))

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.store:
            return ""
        pairs = self.store[key]
        i = bisect.bisect_right(pairs, (timestamp, chr(127)))
        return pairs[i - 1][1] if i > 0 else ""
```

---

## Example Run

Input:

```python
timeMap = TimeMap()
timeMap.set("foo", "bar", 1)
print(timeMap.get("foo", 1))  # Output: "bar"
print(timeMap.get("foo", 3))  # Output: "bar"
timeMap.set("foo", "bar2", 4)
print(timeMap.get("foo", 4))  # Output: "bar2"
print(timeMap.get("foo", 5))  # Output: "bar2"
```

Output:

```
bar
bar
bar2
bar2
```

---

## Complexity Analysis

1. **Set Operation:** `O(1)`
    
    - Appending to the list takes constant time.
2. **Get Operation:** `O(log N)`
    
    - Binary search through the timestamps.
3. **Space Complexity:** `O(N)`
    
    - Store `N` key-value pairs.

---

## Edge Cases

1. No values for the key → Output: `""`
2. Timestamp before any entry → Output: `""`

---

## Conclusion

This solution efficiently handles multiple timestamped values per key using binary search for quick retrieval.