# Solution to "876. Middle of the Linked List"

## Problem Statement

Given the head of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return the second middle node.

Example:

```
Input: head = [1, 2, 3, 4, 5]
Output: [3, 4, 5]
```

Example with even nodes:

```
Input: head = [1, 2, 3, 4, 5, 6]
Output: [4, 5, 6]
```

---

## Approach: Slow and Fast Pointer

### Explanation

1. **Two Pointers:** Use two pointers, `slow` and `fast`.
2. **Traversal:**
    - Move `slow` by one step and `fast` by two steps.
    - When `fast` reaches the end, `slow` will be at the middle.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def middleNode(head: ListNode) -> ListNode:
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow
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

result = middleNode(head)
output = []
while result:
    output.append(result.val)
    result = result.next

print(output)
```

Output:

```
[3, 4, 5]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(N)`
    
    - Each node is visited once.
2. **Space Complexity:** `O(1)`
    
    - No extra space used apart from pointers.

---

## Edge Cases

1. Single node → Return the node itself.
2. Even number of nodes → Return the second middle.

---

## Conclusion

The slow and fast pointer approach efficiently finds the middle node in a singly linked list.