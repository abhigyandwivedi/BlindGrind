```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        if list1==None:
            return list2
        elif list2==None:
            return list1
        elif list1.val<list2.val:
            list1.next= self.mergeTwoLists(list1.next,list2)
            return list1
        else:
            list2.next= self.mergeTwoLists(list1,list2.next)
            return list2

        
```


 
Time complexity  O(n+m)
Space Complexity O(n+m)

#Recursion #recursion
# Solution to "21. Merge Two Sorted Lists"

## Problem Statement

Merge two sorted linked lists and return it as a sorted list. The merged list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

---

## Approach: Recursive Merge

### Explanation

1. **Recursive Comparison:**
    - Compare the heads of the two lists.
    - The smaller node becomes the next node of the merged list.
    - Recursively merge the remaining nodes.
2. **Base Case:**
    - If either list is empty, return the other list.

---

## Implementation in Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def mergeTwoLists(list1, list2):
    if not list1:
        return list2
    if not list2:
        return list1

    if list1.val < list2.val:
        list1.next = mergeTwoLists(list1.next, list2)
        return list1
    else:
        list2.next = mergeTwoLists(list1, list2.next)
        return list2

# Example usage
list1 = ListNode(1, ListNode(2, ListNode(4)))
list2 = ListNode(1, ListNode(3, ListNode(4)))
merged_list = mergeTwoLists(list1, list2)
```

---

## Complexity Analysis

1. **Time Complexity:** `O(n + m)` - `n` and `m` are the lengths of the two lists. Each node is processed once.
2. **Space Complexity:** `O(n + m)` - Due to recursive stack depth.

---

## Example Run

Input:

```
list1 = [1,2,4]
list2 = [1,3,4]
```

Output:

```
[1,1,2,3,4,4]
```

---

## Edge Cases

1. One list is empty returns the other list.
2. Both lists are empty returns `None`.

---

## Conclusion

This solution efficiently merges two sorted linked lists using a recursive approach, ensuring the merged list remains sorted.