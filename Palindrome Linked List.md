# Solution to "234. Palindrome Linked List"

## Problem Statement

Given the head of a singly linked list, return `true` if it is a palindrome, otherwise return `false`.

---

## Approach: Fast and Slow Pointers with Reversal

### Explanation

We can solve this problem in the following steps:

1. **Find the Middle:**
    
    - Use two pointers, `slow` and `fast`.
    - Move `slow` by one step and `fast` by two steps until `fast` reaches the end.
    - `slow` will now point to the middle of the linked list.
2. **Reverse the Second Half:**
    
    - Reverse the second half of the list starting from `slow`.
3. **Compare Both Halves:**
    
    - Compare the first half with the reversed second half.
4. **Restore (Optional):**
    
    - Reverse the second half back to its original form if needed.

### Example Walkthrough

For example, given the linked list:

```
1 -> 2 -> 2 -> 1
```

1. Find middle: `slow` points to the first `2`.
2. Reverse second half: `1 -> 2` becomes `2 -> 1`.
3. Compare both halves: `1 -> 2` equals `2 -> 1` (reversed).
4. Return `true`.

---

## Implementation in Python

```python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if not head or not head.next:
            return True

        # Step 1: Find middle
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next

        # Step 2: Reverse second half
        prev = None
        while slow:
            next_node = slow.next
            slow.next = prev
            prev = slow
            slow = next_node

        # Step 3: Compare both halves
        left, right = head, prev
        while right:
            if left.val != right.val:
                return False
            left = left.next
            right = right.next

        return True
```

---

## Example Run

Input:

```python
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(2)
head.next.next.next = ListNode(1)

solution = Solution()
print(solution.isPalindrome(head))
```

Output:

```
True
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n)`
    
    - Finding the middle takes `O(n/2)`.
    - Reversing the second half takes `O(n/2)`.
    - Comparing takes `O(n/2)`.
    - Total: `O(n)`.
2. **Space Complexity:** `O(1)`
    
    - In-place reversal requires constant extra space.

---

## Edge Cases

1. An empty list is a palindrome.
2. A single-node list is a palindrome.
3. Lists like `1 -> 2 -> 3` return `false`.

---

## Conclusion

This efficient approach checks if a linked list is a palindrome using fast/slow pointers and in-place reversal.