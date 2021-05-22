# 82. Remove Duplicates from Sorted List II

Given the `head` of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list*. Return *the linked list **sorted** as well*.

## Example 1:
![linked_list_1](src/linkedlist1.jpg)
```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

## Example 2:
![linked_list_2](src/linkedlist2.jpg)
```
Input: head = [1,1,1,2,3]
Output: [2,3]
```

## Constraints:
- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is guaranteed to be **sorted** in ascending order.

# Solutiom
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        ans = ListNode(-101, head)
        ptr = ans
        latest = ans
        while ptr.next:
            ptr = ptr.next
            if (not ptr.next) or (ptr.val != ptr.next.val):
                latest.next = ptr
                latest = latest.next
            else:
                while ptr.next and ptr.val == ptr.next.val:
                    ptr = ptr.next
        latest.next = None
        return ans.next
```
Simple Linked List manipulation.
