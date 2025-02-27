# Solution to "2. Add Two Numbers"

## Problem Statement

Given two non-empty linked lists representing two non-negative integers, add the two numbers and return the sum as a linked list. The digits are stored in reverse order, and each node contains a single digit.

---

## Approach: Linked List Traversal

### Explanation

We traverse both linked lists, add corresponding digits, and manage the carry for each addition.

### Algorithm Steps

1. **Initialize:** Create a dummy node and a current pointer. Set `carry` to `0`.
    
2. **Traverse Both Lists:**
    
    - Add corresponding digits from both lists along with the `carry`.
    - Store the unit place in the new node and update the `carry`.
3. **Handle Remaining Carry:** If `carry > 0` after traversal, add a new node with the carry value.
    

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummy = ListNode()
        current = dummy
        carry = 0

        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0

            total = val1 + val2 + carry
            carry, digit = divmod(total, 10)

            current.next = ListNode(digit)
            current = current.next

            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next

        return dummy.next
```

---

## Example Run

Input:

```python
l1 = ListNode(2, ListNode(4, ListNode(3)))  # 342
l2 = ListNode(5, ListNode(6, ListNode(4)))  # 465

result = Solution().addTwoNumbers(l1, l2)

# Print the resulting linked list
while result:
    print(result.val, end=' -> ')
    result = result.next
```

Output:

```
7 -> 0 -> 8 ->
```

---

## Complexity Analysis

1. **Time Complexity:** `O(max(m, n))`
    
    - `m` and `n` are the lengths of the input lists.
2. **Space Complexity:** `O(max(m, n))`
    
    - Extra space for the result linked list.

---

## Edge Cases

1. Different lengths → Proper handling with zeros.
2. Carry at the end → New node added.
3. Single node lists → Proper summation.

---

## Conclusion

This solution efficiently adds two numbers represented by linked lists, handling different lengths and carry propagation.