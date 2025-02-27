# Solution to "148. Sort List"

## Problem Statement

Given the head of a linked list, return the list after sorting it in ascending order.

---

## Approach: Merge Sort (Top-Down)

### Explanation

We can efficiently sort a linked list using the merge sort algorithm, which works well with linked lists due to their structure.

### Algorithm Steps

1. **Base Case:**
    
    - If the list is empty or has only one node, return the head.
2. **Split the List:**
    
    - Use the slow and fast pointer approach to find the middle node.
3. **Sort Both Halves:**
    
    - Recursively sort the left and right halves.
4. **Merge Sorted Halves:**
    
    - Merge the two sorted halves into one sorted list.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        # Function to find the middle node
        def get_middle(node):
            slow, fast = node, node.next
            while fast and fast.next:
                slow = slow.next
                fast = fast.next.next
            return slow

        # Function to merge two sorted lists
        def merge(l1, l2):
            dummy = ListNode()
            current = dummy
            while l1 and l2:
                if l1.val < l2.val:
                    current.next = l1
                    l1 = l1.next
                else:
                    current.next = l2
                    l2 = l2.next
                current = current.next
            current.next = l1 or l2
            return dummy.next

        # Split the list into halves
        middle = get_middle(head)
        right_head = middle.next
        middle.next = None

        # Recursively sort both halves
        left = self.sortList(head)
        right = self.sortList(right_head)

        # Merge sorted halves
        return merge(left, right)
```

---

## Example Run

Input:

```python
head = ListNode(4, ListNode(2, ListNode(1, ListNode(3))))
sorted_list = Solution().sortList(head)

# Print sorted list
while sorted_list:
    print(sorted_list.val, end=' -> ')
    sorted_list = sorted_list.next
```

Output:

```
1 -> 2 -> 3 -> 4 ->
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n log n)`
    
    - Each split takes `O(log n)` and merging takes `O(n)`.
2. **Space Complexity:** `O(log n)`
    
    - Recursive call stack depth.

---

## Edge Cases

1. Empty list → Output: `None`.
2. Single node → Already sorted.
3. Reverse sorted list → Properly sorted.

---

## Conclusion

This solution efficiently sorts a linked list using the merge sort algorithm with optimal time complexity `O(n log n)` and space complexity `O(log n)` due to recursion.