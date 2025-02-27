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
    count = Counter(words)  # O(N)
    
    # Step 2: Use a heap to store words sorted by frequency and lexicographical order
    heap = []
    
    for word, freq in count.items():  # O(M)
        heapq.heappush(heap, (freq, word))  # O(log M)
        if len(heap) > k:
            heapq.heappop(heap)  # O(log M)
    
    # Step 3: Extract words from the heap, sorting by frequency descending and lexicographically
    result = []
    while heap:  # O(k log k)
        result.append(heapq.heappop(heap)[1])
    
    return result[::-1]  # Reverse because heapq produces the elements in ascending order

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
for word, freq in count.items():
	heapq.heappush(heap, (freq, word))
	if len(heap) > k:
	    heapq.heappop(heap)
```

- **M** is the number of unique words.
- **Each `heappush()` takes O(log k)** because the heap has at most `k` elements.
- **Each `heappop()` takes O(log k)** and is called when the heap exceeds `k` elements.
- The loop runs **O(M)** times.

👉 **Total complexity: O(M log k)**

### **3. Extracting k elements from the heap (`heappop()`)**
```python
while heap:
    result.append(heapq.heappop(heap)[1])
```
- Extracting `k` elements from the heap takes **O(k log k)**.

### **4. Reversing the List**
```python
return result[::-1]
```
- Reversing a list of `k` elements takes **O(k)**.

---

### **Overall Time Complexity**

| Step                      | Complexity                   |
| ------------------------- | ---------------------------- |
| Counting word frequencies | **O(N)**                     |
| Inserting into heap       | **O(M log k)**               |
| Extracting from heap      | **O(k log k)**               |
| Reversing the list        | **O(k)**                     |
| **Total Complexity**      | **O(N + M log k + k log k)** |

Since `M ≤ N` in the worst case, we can approximate it as:

👉 **Final Time Complexity: O(N log k)**  
This is significantly **faster than O(N log N)** for large inputs.

---

## **Detailed Space Complexity Analysis**

### **1. Storage for `Counter`**
```python
count = Counter(words)
```
- Stores **M** unique words → **O(M)**.

### **2. Min-Heap Storage**
```python
heap = []
```
- Stores at most **k** elements → **O(k)**.

### **3. Output List**
```python
result = []
```
- Stores **k** elements → **O(k)**.

### **Overall Space Complexity**

| Component            | Space Complexity |
| -------------------- | ---------------- |
| `Counter` Dictionary | **O(M)**         |
| Min-Heap             | **O(k)**         |
| Output List          | **O(k)**         |
| **Total Complexity** | **O(M + k)**     |

Since `M ≤ N`, worst-case space complexity is:

👉 **Final Space Complexity: O(N + k)**

---

## **Final Summary**

| Approach                   | Time Complexity | Space Complexity |
| -------------------------- | --------------- | ---------------- |
| **Sorting-Based**          | **O(N log N)**  | **O(N + k)**     |
| **Heap-Based** (Optimized) | **O(N log k)**  | **O(N + k)**     |

🔹 **Heap-based approach is more efficient** than sorting for large values of `N`, especially when `k << N`, because it avoids full sorting. 🚀