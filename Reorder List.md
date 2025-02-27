# LeetCode 143: Reorder List

## Problem Statement

Given the head of a singly linked list, reorder the list to be in the following form:

```
L0 → L1 → Ln → L(n-1) → L2 → L(n-2) → …
```

You may not modify the values in the list's nodes, only the node structure itself.

---

## Example

### Example 1

```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

### Example 2

```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

---

## Approach

We can break down the solution into three main steps:

1. **Find the middle of the list:** Use the slow and fast pointer technique to locate the middle node.
2. **Reverse the second half:** Reverse the second half of the linked list.
3. **Merge the two halves:** Merge the first half with the reversed second half.

---

## Solution (Python)

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reorderList(head: ListNode) -> None:
    if not head:
        return

    # Step 1: Find the middle of the list
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    # Step 2: Reverse the second half of the list
    prev, curr = None, slow
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp

    # Step 3: Merge the two halves
    first, second = head, prev
    while second.next:
        tmp1, tmp2 = first.next, second.next
        first.next, second.next = second, tmp1
        first, second = tmp1, tmp2
```

---

## Detailed Explanation

### Step 1: Find the middle of the list

We use the slow and fast pointer technique. The `slow` pointer moves one step at a time, while the `fast` pointer moves two steps. When `fast` reaches the end, `slow` will be at the middle of the list.

Example:

```
Input: 1 → 2 → 3 → 4 → 5
After finding middle: slow points to 3
```

### Step 2: Reverse the second half of the list

We reverse the list starting from the middle node.

Example:

```
Original Second Half: 3 → 4 → 5
Reversed Second Half: 5 → 4 → 3
```

### Step 3: Merge the two halves

We merge the first half with the reversed second half by alternately linking nodes from each half.

Example:

```
First half: 1 → 2 → 3
Reversed second half: 5 → 4 → 3
Merged list: 1 → 5 → 2 → 4 → 3
```

---

## Complexity Analysis

### Time Complexity: O(N)

- **Finding the middle:** O(N/2) → O(N)
- **Reversing the second half:** O(N/2) → O(N)
- **Merging the halves:** O(N) Thus, the total time complexity is **O(N)**.

### Space Complexity: O(1)

We only use a few pointers (`slow`, `fast`, `prev`, `curr`), which means constant extra space.

---

## Edge Cases

1. **Empty list:** If `head` is `None`, nothing changes.
2. **Single node:** If only one node exists, no reordering is required.
3. **Even-length list:** Properly alternates the order.
4. **Odd-length list:** Middle node stays in place.

---

## Example Run

For the input `1 → 2 → 3 → 4 → 5`, the output will be:

```
1 → 5 → 2 → 4 → 3
```

For the input `1 → 2 → 3 → 4`, the output will be:

```
1 → 4 → 2 → 3
```

---

## Conclusion

This solution efficiently reorders the list with linear time complexity and constant space complexity, maintaining the node structure without altering node values.