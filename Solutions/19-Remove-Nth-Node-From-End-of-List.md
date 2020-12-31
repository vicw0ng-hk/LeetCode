# 19. Remove Nth Node From End of List

Given the `head` of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.

**Follow up**: Could you do this in one pass?

## Example 1:

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

## Example 2:
```
Input: head = [1], n = 1
Output: []
```

## Example 3:
```
Input: head = [1,2], n = 1
Output: [1]
```

Constraints:
- The number of nodes in the list is `sz`
- `1 <= sz <= 30`
- `0 <= Node.val <= 100`
- `1 <= n <= sz`

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        start = ListNode()
        start.next = head
        ptr1, ptr2 = start, start
        for _ in range(n):
            ptr1 = ptr1.next
        while ptr1.next != None:
            ptr1 = ptr1.next
            ptr2 = ptr2.next
        if ptr2.next == head:
            ptr2.next = ptr2.next.next
            return ptr2.next
        else:
            ptr2.next = ptr2.next.next
            return head
```
One pass with two pointers.
