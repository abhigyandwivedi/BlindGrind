# 🔄 Rotate List (LeetCode 61)

## 🚀 Problem Statement

Given the head of a linked list, rotate the list to the right by `k` places.

### 🔑 Example:

```python
Input: head = [1, 2, 3, 4, 5], k = 2
Output: [4, 5, 1, 2, 3]
Explanation: Rotating the list to the right by 2 places gives [4, 5, 1, 2, 3].
```

---

## 📝 **Optimized O(n) Solution**

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

from typing import Optional

def rotateRight(head: Optional[ListNode], k: int) -> Optional[ListNode]:
    if not head or not head.next or k == 0:
        return head

    # Step 1: Find the length of the linked list
    length = 1
    tail = head
    while tail.next:
        tail = tail.next
        length += 1

    # Step 2: Calculate the effective rotations needed
    k = k % length
    if k == 0:
        return head

    # Step 3: Find the new tail (length - k - 1) and new head (length - k)
    new_tail = head
    for _ in range(length - k - 1):
        new_tail = new_tail.next

    new_head = new_tail.next
    new_tail.next = None
    tail.next = head  # Connect the original tail to the original head

    return new_head

# Example usage
# Input: 1 -> 2 -> 3 -> 4 -> 5, k = 2
# Output: 4 -> 5 -> 1 -> 2 -> 3
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
head.next.next.next = ListNode(4)
head.next.next.next.next = ListNode(5)
k = 2

result = rotateRight(head, k)
while result:
    print(result.val, end=" -> " if result.next else "\n")
    result = result.next
```

---

## ⏱️ **Time Complexity Analysis**

1. **Find Length:** Traversing the list takes O(n)O(n) time.
2. **Effective Rotation:** Calculating `k % length` takes O(1)O(1).
3. **Finding New Head:** Another traversal to find the new head takes O(n)O(n).

Thus, the overall time complexity is:

O(n)O(n)

Where `n` is the length of the linked list.

---

## 💾 **Space Complexity Analysis**

- **In-place Rotation:** No additional data structures are used aside from pointers.
- **Auxiliary Variables:** Constant space for variables like `length`, `new_tail`, and `new_head`.

Thus, the overall space complexity is:

O(1)O(1)

---

## ✅ **Key Insights:**

1. Rotating by `k` places is equivalent to rotating by `k % n` places.
2. Efficient two-pass approach ensures linear complexity.
3. Properly managing pointers avoids creating new nodes.
4. O(n)O(n) time and O(1)O(1) space are optimal for linked list manipulations.