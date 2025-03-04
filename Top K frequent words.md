 #heaps #pythonfrequentwordsK #topkfrequentwords #heaps
 
Leetcode problem link
https://leetcode.com/problems/top-k-frequent-words/description/


```python
from collections import Counter

def topKFrequent(words, k):
    # Count the frequency of each word
    count = Counter(words)
    # Sort words by frequency and then alphabetically
    sorted_words = sorted(count.keys(), key=lambda word: (-count[word], word))
    # Return the top k words
    return sorted_words[:k]

# Example Usage
words = ["i", "love", "leetcode", "i", "love", "coding"]
k = 2
print(topKFrequent(words, k))  # Output: ['i', 'love']

# 🔥 Example Runs
print(topKFrequent(["i", "love", "leetcode", "i", "love", "coding"], 2))
# Output: ["i", "love"]

print(
    topKFrequent(
        ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"],
        4,
    )
)
```

## **Time Complexity Analysis**

We break the function into its major operations:

### **1. Counting word frequencies (`Counter(words)`)**

```python
count = Counter(words)
```

- Constructing a frequency dictionary (`Counter`) requires iterating over `words` once.
- **Time Complexity: O(N)**, where **N** is the total number of words in `words`.

### **2. Sorting words**
```python
sorted_words = sorted(count.keys(), key=lambda word: (-count[word], word))
```

- `count.keys()` returns a list of unique words.
- Let **M** be the number of unique words.
- Sorting involves:
    - Comparing words by frequency (`-count[word]`), which is **O(1)** per word.
    - If frequencies are the same, comparing words lexicographically takes **O(W)** per comparison (where **W** is the average word length).
- Sorting **M** words takes **O(M log M)**.

### **3. Slicing the sorted list**
```python
return sorted_words[:k]
```

- Extracting the first `k` elements takes **O(k)**.

### **Overall Time Complexity**

- Counting words: **O(N)**
- Sorting words: **O(M log M)**
- Slicing the list: **O(k)** (negligible compared to sorting)

Since `M ≤ N` (worst case: all words are unique), we approximate the complexity as:

**O(N + N log N) = O(N log N) in the worst case.**

---

## **Space Complexity Analysis**

### **1. Storage for `Counter`**
```python
count = Counter(words)
```

- Stores **M** unique words and their counts → **O(M)** space.

### **2. Storage for `sorted_words`**
```python
sorted_words = sorted(count.keys(), key=lambda word: (-count[word], word))
```

- Stores **M** unique words → **O(M)** space.

### **3. Return list**
```python
return sorted_words[:k] 
```

- Returns a list of **k** words → **O(k)** space.

### **Overall Space Complexity**

- **O(M)** for `Counter`
- **O(M)** for sorting
- **O(k)** for output list
- **Total: O(M + k)**  
    Since `M ≤ N`, worst-case space complexity is **O(N + k)**.

---

## **Final Complexity Summary**

- **Time Complexity:** **O(N log N)**
- **Space Complexity:** **O(N + k)**


******************************************************
# Heap based approach:
```python
from collections import Counter
import heapq

def topKFrequent(words, k):
    # Step 1: Count the frequency of each word
    count = Counter(words)
    
    # Step 2: Use a max-heap (negative frequency to make it max-heap)
    heap = [(-freq, word) for word, freq in count.items()]
    heapq.heapify(heap)  # O(M) to heapify all elements

    # Step 3: Extract the top k elements from the heap
    result = [heapq.heappop(heap)[1] for _ in range(k)]  # O(k log M)
    
    return result

# Example Usage
print(topKFrequent(["i", "love", "leetcode", "i", "love", "coding"], 2))  
# Output: ['i', 'love']

print(topKFrequent(["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], 4))  
# Output: ['the', 'is', 'sunny', 'day']
```

## **Detailed Time Complexity Analysis**

Let's analyze each step carefully:

### **1. Counting word frequencies (`Counter(words)`)**
```python 
count = Counter(words)
```
- Constructing a frequency dictionary takes **O(N)** time because we iterate through `words` once.

### **2. Constructing a Min-Heap (`heapq.heappush`)**
```python
heap = [(-freq, word) for word, freq in count.items()]
heapq.heapify(heap)
```
- **M** is the number of unique words.
- `heapify` builds the heap in **O(M)** time.

👉 **Total complexity: O(M)**

### **3. Extracting k elements from the heap (`heappop()`)**
```python
result = [heapq.heappop(heap)[1] for _ in range(k)]
```
- Extracting `k` elements from the heap takes **O(k log M)**.

---

### **Overall Time Complexity**

| Step                      | Complexity                   |
| ------------------------- | ---------------------------- |
| Counting word frequencies | **O(N)**                     |
| Heapify operation         | **O(M)**                     |
| Extracting from heap      | **O(k log M)**               |
| **Total Complexity**      | **O(N + M + k log M)**       |

Since `M ≤ N` in the worst case, we can approximate it as:

👉 **Final Time Complexity: O(N + k log M)**  
This is significantly **faster than O(N log N)** for large inputs.

---

## **Detailed Space Complexity Analysis**

### **1. Storage for `Counter`**
```python
count = Counter(words)
```
- Stores **M** unique words → **O(M)**.

### **2. Heap Storage**
```python
heap = [(-freq, word) for word, freq in count.items()]
```
- Stores **M** elements → **O(M)**.

### **3. Output List**
```python
result = []
```
- Stores **k** elements → **O(k)**.

### **Overall Space Complexity**

| Component            | Space Complexity |
| -------------------- | ---------------- |
| `Counter` Dictionary | **O(M)**         |
| Heap Storage        | **O(M)**         |
| Output List         | **O(k)**         |
| **Total Complexity** | **O(M + k)**     |

Since `M ≤ N`, worst-case space complexity is:

👉 **Final Space Complexity: O(N + k)**

---

## **Final Summary**

| Approach                   | Time Complexity | Space Complexity |
| -------------------------- | --------------- | ---------------- |
| **Sorting-Based**          | **O(N log N)**  | **O(N + k)**     |
| **Heap-Based** (Optimized) | **O(N + k log M)**  | **O(N + k)**     |

🔹 **Heap-based approach is more efficient** than sorting for large values of `N`, especially when `k << N`, because it avoids full sorting. 🚀