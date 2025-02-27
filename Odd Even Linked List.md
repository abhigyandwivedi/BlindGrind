# Solution to "328. Odd Even Linked List"

## Problem Statement

Given the head of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

---

## Approach: Two Pointers

### Explanation

1. Use two pointers: `odd` for odd-indexed nodes and `even` for even-indexed nodes.
2. Iterate through the list, connecting odd nodes to the next odd and even nodes to the next even.
3. After traversing, connect the last odd node to the head of the even list.

### Algorithm Steps

1. **Initialization:** Set `odd` to `head` and `even` to `head.next`.
2. **Iteration:**
    - Connect `odd.next` to `even.next` and move `odd` forward.
    - Connect `even.next` to `odd.next` and move `even` forward.
3. **Final Connection:** Connect the last odd node to the head of the even list.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        odd, even = head, head.next
        even_head = even

        while even and even.next:
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next

        odd.next = even_head
        return head
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

solution = Solution()
result = solution.oddEvenList(head)

while result:
    print(result.val, end=" -> ")
    result = result.next
```

Output:

```
1 -> 3 -> 5 -> 2 -> 4 ->
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is processed once.
2. **Space Complexity:** `O(1)`
    
    - Reordering is done in-place.

---

## Edge Cases

1. Single node → No change.
2. Empty list → Return `None`.
3. Two nodes → Already ordered.

---

## Conclusion

This solution efficiently rearranges the linked list into odd-indexed nodes followed by even-indexed nodes using a two-pointer approach.