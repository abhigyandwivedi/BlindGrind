# 380. Insert Delete GetRandom O(1)

## 📝 Problem Statement

Design a data structure that supports all of the following operations in **average O(1)** time complexity:

1. **Insert(val):** Inserts an item `val` into the set if it is not already present.
2. **Remove(val):** Removes an item `val` from the set if it is present.
3. **GetRandom():** Returns a random element from the set. Each element must have the same probability of being returned.

## 🌟 Approach

To achieve O(1) complexity for all operations, we'll use two data structures:

1. **HashMap (Dictionary):** To store the value-to-index mapping.
2. **Array (List):** To store the elements.

### 🔑 Key Insights

- **Insert:** Append the element to the list and store its index in the hashmap.
- **Remove:** Swap the element to be removed with the last element, update indices in the hashmap, and pop the last element.
- **GetRandom:** Use Python's `random.choice()` or pick a random index from the array.

## 🖨️ Implementation (Python Example)

```python
import random

class RandomizedSet:
    def __init__(self):
        self.data = []  # List to store elements
        self.idx_map = {}  # HashMap to store value -> index

    def insert(self, val: int) -> bool:
        if val in self.idx_map:
            return False
        self.data.append(val)
        self.idx_map[val] = len(self.data) - 1
        return True

    def remove(self, val: int) -> bool:
        if val not in self.idx_map:
            return False
        last_element = self.data[-1]
        idx_to_remove = self.idx_map[val]
        # Swap the last element with the element to be removed
        self.data[idx_to_remove] = last_element
        self.idx_map[last_element] = idx_to_remove
        # Remove the last element
        self.data.pop()
        del self.idx_map[val]
        return True

    def getRandom(self) -> int:
        return random.choice(self.data)
```

## ⏱️ Time Complexity Analysis

|Operation|Time Complexity|Explanation|
|---|---|---|
|**Insert**|O(1)|Appending to the list and updating hashmap.|
|**Remove**|O(1)|Swap with the last element, update hashmap, pop.|
|**GetRandom**|O(1)|Random access using array indexing.|

## 🗄️ Space Complexity Analysis

- **O(N):** Where `N` is the number of inserted elements.
    - The array stores `N` elements.
    - The hashmap stores `N` key-value pairs.

## ✅ Example Run

```python
randomized_set = RandomizedSet()
print(randomized_set.insert(10))  # True
print(randomized_set.insert(20))  # True
print(randomized_set.insert(10))  # False
print(randomized_set.remove(10))  # True
print(randomized_set.getRandom()) # Randomly returns 20
```

## ⚙️ Edge Cases

1. Inserting an existing value → Returns `False`.
2. Removing a non-existing value → Returns `False`.
3. Calling `getRandom()` on an empty set → Raises an exception (handle it if needed).

## 🚀 Conclusion

By combining a hashmap for O(1) lookups and a list for O(1) random access, we achieve constant-time complexity for insert, delete, and getRandom operations efficiently.