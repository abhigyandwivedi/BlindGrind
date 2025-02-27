# Solution to "24. Swap Nodes in Pairs"

## Problem Statement

Given a linked list, swap every two adjacent nodes and return its head.

You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed).

---

## Approach: Iterative Approach

### Explanation

1. Create a dummy node pointing to the head of the list.
2. Use a pointer `prev` starting from the dummy node.
3. Swap each pair of nodes by adjusting the pointers.
4. Move `prev` two steps forward after each swap.

### Algorithm Steps

1. Initialize a dummy node before the head.
2. Iterate through the list while there are pairs to swap.
3. Swap the current pair and adjust pointers.
4. Move to the next pair.
5. Return the new head.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        prev = dummy

        while prev.next and prev.next.next:
            first = prev.next
            second = first.next

            # Swapping
            first.next = second.next
            second.next = first
            prev.next = second

            # Move to the next pair
            prev = first

        return dummy.next
```

---

## Example Run

Input:

```python
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
head.next.next.next = ListNode(4)

solution = Solution()
new_head = solution.swapPairs(head)

# Print result
current = new_head
while current:
    print(current.val, end=" -> ")
    current = current.next
```

Output:

```
2 -> 1 -> 4 -> 3 -> 
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(1)`
    
    - No extra space used except for pointers.

---

## Edge Cases

1. Empty list → Result is `[]`.
2. Single node → No swap, return as is.
3. Even/odd length lists → Only pairs are swapped.

---

## Conclusion

This solution efficiently swaps adjacent nodes in a linked list using an iterative approach without modifying node values.