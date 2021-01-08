# 61. Rotate List

Given the `head` of a linked list, rotate the list to the right by `k` places.

## Example 1:
```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

## Example 2:
```
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

## Constraints:
- The number of nodes in the list is in the range `[0, 500]`.
- `-100 <= Node.val <= 100`
- <code>0 <= k <= 2 * 10<sup>9</sup></code>

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not head:
            return None
        ans = ListNode()
        ans.next = head
        length, ptr = 0, ans
        while ptr.next != None:
            length += 1
            ptr = ptr.next
        k %= length
        if k == 0:
            return ans.next
        old_end = ptr
        new_end = ans
        for _ in range(length-k):
            new_end = new_end.next
        old_end.next = ans.next
        ans.next = new_end.next
        new_end.next = None
        return ans.next
```
Some Linked List operation.
