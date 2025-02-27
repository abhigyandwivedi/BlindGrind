# Smallest Range Covering Elements from K Lists

## **Problem Statement**

Given kk sorted lists of integers, find the smallest range [a,b][a, b] such that at least one number from each of the kk lists falls within this range.

### **Example:**

Input:

```python
nums = [
  [4, 10, 15, 24, 26],
  [0, 9, 12, 20],
  [5, 18, 22, 30]
]
```

Output:

```
[20, 24]
```

Explanation:

- The range [20, 24] includes at least one element from each list:
    - From the first list: 24
    - From the second list: 20
    - From the third list: 22

---

## **Approach using Priority Queue (Min-Heap)**

### **1. Core Idea:**

- We maintain a **min-heap** (priority queue) to keep track of the smallest current element across the lists.
- Simultaneously, we track the **current maximum** element among the elements in the heap.
- Our goal is to continuously update the range [a,b][a, b] based on the current minimum and maximum.

### **2. Steps:**

1. **Heap Initialization:**
    
    - Create a min-heap where each entry is a tuple (num,i,j)(num, i, j), where:
        - `num`: The current element from the iith list at index jj.
        - `i`: The index of the list the element belongs to.
        - `j`: The current index within the list.
    - Push the first element from each list into the heap.
    - Track the current maximum element among the entries in the heap.
2. **Heap Processing:**
    
    - Continuously pop the smallest element from the heap.
    - Update the range [min,max][min, max] if the current range is smaller.
    - Move to the next element in the same list as the popped element.
    - Update the current maximum if the new element is larger.
    - If any list is exhausted, break the loop.
3. **Output the Smallest Range:**
    
    - The smallest range [a,b][a, b] is the one found during the heap operations.

---

## **Python Code Implementation**

```python
import heapq

def smallestRange(nums):
    # Min-heap to store (value, list_index, element_index)
    min_heap = []
    current_max = float('-inf')
    
    # Initialize the heap with the first element of each list
    for i, lst in enumerate(nums):
        heapq.heappush(min_heap, (lst[0], i, 0))
        current_max = max(current_max, lst[0])
    
    # Initialize the best range
    best_range = [float('-inf'), float('inf')]
    
    # Process the heap
    while min_heap:
        current_min, i, j = heapq.heappop(min_heap)
        
        # Update the range if it's smaller than the previous best range
        if current_max - current_min < best_range[1] - best_range[0]:
            best_range = [current_min, current_max]
        
        # Move to the next element in the same list
        if j + 1 < len(nums[i]):
            next_val = nums[i][j + 1]
            heapq.heappush(min_heap, (next_val, i, j + 1))
            current_max = max(current_max, next_val)
        else:
            # If any list is exhausted, we can't cover all lists
            break
    
    return best_range

# Example usage
nums = [
    [4, 10, 15, 24, 26],
    [0, 9, 12, 20],
    [5, 18, 22, 30]
]

print("Smallest Range:", smallestRange(nums))
```

---

## **Output:**

```
Smallest Range: [20, 24]
```

---

## **Detailed Walkthrough of Execution:**

### **Initialization:**

- We start by pushing the first element from each list into the min-heap:

```
Heap: [(4, 0, 0), (0, 1, 0), (5, 2, 0)]
Current Max: 5
```

- The heap is ordered by the first value in each tuple.

### **Iteration 1:**

1. Pop the smallest element: `(0, 1, 0)` (from the second list).
2. Update the current range: `[0, 5]`.
3. Push the next element from the second list: `9`.
4. Update current max: `9`.

Heap after iteration 1:

```
Heap: [(4, 0, 0), (5, 2, 0), (9, 1, 1)]
Current Max: 9
```

### **Iteration 2:**

1. Pop `(4, 0, 0)`.
2. Update range: `[4, 9]` (smaller than previous range).
3. Push next element from first list: `10`.
4. Update current max: `10`.

Heap after iteration 2:

```
Heap: [(5, 2, 0), (9, 1, 1), (10, 0, 1)]
Current Max: 10
```

Continue this process until one list is exhausted.

---

## **Complexity Analysis:**

### **Time Complexity:** O(Nlog⁡k)O(N \log k)

- NN: Total number of elements across all lists.
- kk: Number of lists.
- Each insertion and deletion from the heap takes O(log⁡k)O(\log k), and we process all elements once.

### **Space Complexity:** O(k+N)O(k + N)

- O(k)O(k): The heap stores one element from each list at any time.
- O(N)O(N): In the worst case, all elements from the lists could be processed and stored momentarily.

---

## **Edge Cases:**

1. **Single List:** If only one list is provided, the smallest range is the first and last element of that list.
2. **Uneven List Sizes:** The algorithm works even if lists have different lengths.
3. **Empty Lists:** If any list is empty, it's impossible to find a valid range.

---

## **Conclusion:**

Using a priority queue allows us to efficiently find the smallest range covering elements from multiple sorted lists. By keeping track of the current minimum and maximum, we ensure that the solution is optimal both in terms of time and space complexity.

Would you like to see the solution implemented in another programming language, like Rust or C++?