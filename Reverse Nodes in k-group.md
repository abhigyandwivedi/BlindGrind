# 25.Reverse Nodes in k-Group

## Problem Statement

Given the head of a linked list, reverse the nodes of the list k at a time and return the modified list. k is a positive integer, and the nodes are reversed in groups of k. If the number of nodes is not a multiple of k, leave the remaining nodes as they are.

## Solution

Here's the Python solution to reverse nodes in k-group.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverseKGroup(head: ListNode, k: int) -> ListNode:
    def reverse_linked_list(start, end):
        prev, curr = end, start
        while curr != end:
            tmp = curr.next
            curr.next = prev
            prev = curr
            curr = tmp
        return prev

    dummy = ListNode(0)
    dummy.next = head
    prev_group_end = dummy

    while True:
        # Find the k-th node
        kth_node = prev_group_end
        for _ in range(k):
            if not kth_node.next:
                return dummy.next
            kth_node = kth_node.next

        # Reverse k nodes
        group_start = prev_group_end.next
        next_group_start = kth_node.next
        kth_node.next = None

        prev_group_end.next = reverse_linked_list(group_start, None)
        group_start.next = next_group_start

        prev_group_end = group_start

    return dummy.next
```

## Example Usage

```python
# Example Linked List: 1 -> 2 -> 3 -> 4 -> 5
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
head.next.next.next = ListNode(4)
head.next.next.next.next = ListNode(5)

k = 2
new_head = reverseKGroup(head, k)

# Print the reversed list
current = new_head
while current:
    print(current.val, end=" -> ")
    current = current.next
```

Output for k = 2:

```
2 -> 1 -> 4 -> 3 -> 5 ->
```

## Time Complexity Analysis

1. **Traversal of the Linked List:** Each node is visited once to form groups of k, leading to a time complexity of O(n), where n is the number of nodes.
2. **Reversing k Nodes:** Each group of k nodes is reversed in O(k) time. Since there are approximately n/k groups, the overall reversal time is O(n).

Thus, the overall time complexity is **O(n)**.

## Space Complexity Analysis

1. **Recursive Stack (if reverse is done recursively):** The stack depth for reversing each group is O(k). However, this solution uses an iterative approach.
2. **Extra Variables:** Only constant space is used for pointers.

Thus, the overall space complexity is **O(1)**, excluding the output list.