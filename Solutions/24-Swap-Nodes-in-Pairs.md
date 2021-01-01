# 24. Swap Nodes in Pairs

Given a linked list, swap every two adjacent nodes and return its head.

You may **not** modify the values in the list's nodes. Only nodes itself may be changed.

## Example 1:

```
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

## Example 2:
```
Input: head = []
Output: []
```

## Example 3:
```
Input: head = [1]
Output: [1]
```

## Constraints:
- The number of nodes in the list is in the range `[0, 100]`
- `0 <= Node.val <= 100`

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        ans = ListNode()
        ans.next = head
        ptr1, ptr2 = ListNode(), ans
        ptr1.next = ptr2
        while ptr2.next and ptr2.next.next:
            tmp = ptr2
            ptr1 = ptr2.next
            ptr2 = ptr1.next
            ptr1.next = ptr2.next
            tmp.next = ptr2
            ptr2.next = ptr1
            ptr1, ptr2 = ptr2, ptr1
        return ans.next
```
Simple linked list operation.
