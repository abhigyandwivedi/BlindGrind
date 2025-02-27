# Solution to "19. Remove Nth Node From End of List"

## Problem Statement

Given the head of a linked list, remove the `n`th node from the end of the list and return its head.

---

## Approach: Two-Pointer Technique

### Explanation

To remove the `n`th node from the end, we use the two-pointer approach:

1. Initialize two pointers, `first` and `second`.
2. Move `first` pointer `n` steps ahead.
3. Move both pointers until `first` reaches the end.
4. `second` will now point to the node before the one to be removed.
5. Adjust the pointers to skip the target node.

### Algorithm Steps

1. Create a dummy node pointing to the head.
2. Move the `first` pointer `n` steps forward.
3. Move both `first` and `second` pointers until `first` reaches the end.
4. Delete the `n`th node by adjusting pointers.
5. Return the new head.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        first = dummy
        second = dummy

        # Move first pointer n steps ahead
        for _ in range(n + 1):
            first = first.next

        # Move both pointers
        while first:
            first = first.next
            second = second.next

        # Remove the nth node
        second.next = second.next.next

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
head.next.next.next.next = ListNode(5)
n = 2

solution = Solution()
new_head = solution.removeNthFromEnd(head, n)

while new_head:
    print(new_head.val, end=" → ")
    new_head = new_head.next
```

Output:

```
1 → 2 → 3 → 5 →
```

Explanation:

- The `2`nd node from the end (`4`) is removed.

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Single pass through the list.
2. **Space Complexity:** `O(1)`
    
    - Constant extra space.

---

## Edge Cases

1. Single node → Remove the only node → Output `None`.
2. Remove head → Adjust dummy node.

---

## Conclusion

This solution efficiently removes the `n`th node from the end of a linked list using the two-pointer technique while ensuring optimal time complexity.