# Solution to "141. Linked List Cycle"

## Problem Statement

Given the `head` of a singly linked list, determine if the linked list has a cycle in it.

Example:

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

---

## Approach: Floyd's Cycle Detection (Tortoise and Hare Algorithm)

### Explanation

1. **Two Pointers:** Use two pointers, `slow` and `fast`.
2. **Movement:** Move `slow` by one step and `fast` by two steps.
3. **Cycle Detection:** If `slow` meets `fast`, a cycle exists. If `fast` reaches `None`, there's no cycle.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def hasCycle(head: ListNode) -> bool:
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

# Example usage
# node1 = ListNode(3)
# node2 = ListNode(2)
# node3 = ListNode(0)
# node4 = ListNode(-4)
# node1.next = node2
# node2.next = node3
# node3.next = node4
# node4.next = node2  # Cycle here
# print(hasCycle(node1))  # Output: True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)` - Each node is visited at most once.
2. **Space Complexity:** `O(1)` - Only constant extra space is used for pointers.

---

## Example Run

Input:

```
head = [3,2,0,-4], pos = 1
```

Output:

```
True
```

---

## Edge Cases

1. Empty list → `False`
2. Single node without cycle → `False`
3. Single node with cycle → `True`

---

## Conclusion

This solution efficiently detects cycles in a linked list using the Floyd's Cycle Detection algorithm, ensuring linear time complexity and constant space complexity.