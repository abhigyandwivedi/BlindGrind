# Solution to "23. Merge k Sorted Lists"

## Problem Statement

You are given an array of `k` linked lists, each sorted in ascending order. Merge all the linked lists into one sorted linked list and return it.

Example:

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
```

---

## Approach: Min-Heap (Priority Queue)

### Explanation

1. **Use a Min-Heap:** Push the head of each list into the heap as a tuple `(value, index, node)`.
2. **Heapify:** Extract the smallest element and add it to the merged list.
3. **Push Next Node:** If the extracted node has a `next`, push it into the heap.
4. **Continue:** Repeat until the heap is empty.

---

## Implementation in Python

```python
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def mergeKLists(lists):
    heap = []

    # Add the head of each list to the heap
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))

    dummy = ListNode()
    current = dummy

    while heap:
        val, i, node = heapq.heappop(heap)
        current.next = node
        current = current.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))

    return dummy.next
```

---

## Example Run

Input:

```python
lists = [
    ListNode(1, ListNode(4, ListNode(5))),
    ListNode(1, ListNode(3, ListNode(4))),
    ListNode(2, ListNode(6))
]

result = mergeKLists(lists)
while result:
    print(result.val, end=" → ")
    result = result.next
```

Output:

```
1 → 1 → 2 → 3 → 4 → 4 → 5 → 6 → None
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N log k)`
    
    - `N` is the total number of nodes.
    - Insertion and extraction from the heap take `O(log k)` time.
2. **Space Complexity:** `O(k)`
    
    - Heap stores at most `k` elements.

---

## Edge Cases

1. Empty list of lists → `None`.
2. Single empty list → `None`.
3. Lists of different lengths → Merges correctly.

---

## Conclusion

Using a min-heap ensures efficient merging of `k` sorted linked lists in logarithmic time complexity.