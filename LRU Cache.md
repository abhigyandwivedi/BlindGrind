	# Solution to "146. LRU Cache"

## Problem Statement

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initializes the LRU cache with positive size `capacity`.
- `int get(int key)` Returns the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, evict the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

---

## Approach: Using Ordered Dictionary

### Explanation

1. **Ordered Dictionary:** Use `collections.OrderedDict` to maintain the order of access.
2. **Get Operation:** If the key exists, move it to the end (most recently used) and return its value.
3. **Put Operation:** If the key exists, update its value and move it to the end. If capacity exceeds, remove the least recently used item (from the beginning).

---

## Implementation in Python

```python
from collections import OrderedDict

class LRUCache:

    def __init__(self, capacity: int):
        self.cache = OrderedDict()
        self.capacity = capacity

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        # Move accessed item to the end
        self.cache.move_to_end(key)
        return self.cache[key]

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            # Remove the old value
            del self.cache[key]
        self.cache[key] = value
        # Move to end as most recently used
        self.cache.move_to_end(key)
        # Evict least recently used if capacity exceeded
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)
```

---

## Example Run

Input:

```python
cache = LRUCache(2)
cache.put(1, 1)
cache.put(2, 2)
print(cache.get(1))  # Returns 1
cache.put(3, 3)      # Evicts key 2
print(cache.get(2))  # Returns -1 (not found)
cache.put(4, 4)      # Evicts key 1
print(cache.get(1))  # Returns -1 (not found)
print(cache.get(3))  # Returns 3
print(cache.get(4))  # Returns 4
```

Output:

```
1
-1
-1
3
4
```

---

## Complexity Analysis

1. **Time Complexity:** `O(1)` for both `get` and `put` operations.
2. **Space Complexity:** `O(capacity)` for storing items in the cache.

---

## Edge Cases

1. Accessing a non-existent key returns `-1`.
2. When capacity is exceeded, the least recently used key gets evicted.

---

## Conclusion

Using an ordered dictionary ensures efficient `O(1)` operations while maintaining the order of access, making it ideal for LRU cache implementation.