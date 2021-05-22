# 83. Remove Duplicates from Sorted List

Given the `head` of a sorted linked list, *delete all duplicates such that each element appears only once*. Return *the linked list **sorted** as well*.

## Example 1:
```
Input: head = [1,1,2]
Output: [1,2]
```

## Example 2:
```
Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

## Constraints:
- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is guaranteed to be **sorted** in ascending order.

# Solution
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
            if ptr.val != latest.val:
                latest.next = ptr
                latest = latest.next
        latest.next = None
        return ans.next
```
Even simpler linked list manipulation. 
