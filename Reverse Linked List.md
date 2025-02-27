# Solution to "206. Reverse Linked List"

## Problem Statement

Given the head of a singly linked list, reverse the list and return its head.

Example:

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Input: head = [1,2]
Output: [2,1]

Input: head = []
Output: []
```

---

## Approach: Iterative and Recursive

### 1. Iterative Approach

**Explanation:**

- Initialize three pointers: `prev` as `None`, `current` as `head`, and `next` for traversal.
- Traverse the list, reversing the pointers at each step.
- Finally, return `prev` as the new head.

**Implementation:**

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverseList(head):
    prev = None
    current = head
    while current:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    return prev

# Example usage
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
print(reverseList(head))  # Output: [3, 2, 1]
```

---

### 2. Recursive Approach

**Explanation:**

- Recursively reverse the rest of the list and link the current node.
- Base case: If `head` is `None` or `head.next` is `None`, return `head`.

**Implementation:**

```python
def reverseListRecursive(head):
    if not head or not head.next:
        return head
    new_head = reverseListRecursive(head.next)
    head.next.next = head
    head.next = None
    return new_head
```

---

## Example Run

Input:

```python
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
print(reverseList(head))
```

Output:

```
[3, 2, 1]
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Each node is visited once.
2. **Space Complexity:**
    
    - Iterative: `O(1)` (constant space for pointers).
    - Recursive: `O(n)` (recursion stack).

---

## Edge Cases

1. Empty list: Return `None`.
2. Single node: Return the same node.
3. Multiple nodes: Reverse properly.

---

## Conclusion

This solution efficiently reverses a singly linked list using both iterative and recursive approaches.