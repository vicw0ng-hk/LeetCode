# 21. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new **sorted** list. The new list should be made by splicing together the nodes of the first two lists.

## Example 1:
![merge_ex1.jpg](/src/merge_ex1.jpg)
```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

## Example 2:
```
Input: l1 = [], l2 = []
Output: []
```

## Example 3:
```
Input: l1 = [], l2 = [0]
Output: [0]
```

## Constraints:
- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `l1` and `l2` are sorted in non-decreasing order.

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        ptr = ListNode()
        ans = ptr
        while True:
            tmp = ListNode()
            if l1 == l2 == None:
                break
            elif not l1:
                tmp.val = l2.val
                l2 = l2.next
            elif not l2:
                tmp.val = l1.val
                l1 = l1.next
            else:
                if l1.val <= l2.val:
                    tmp.val = l1.val
                    l1 = l1.next
                else:
                    tmp.val = l2.val
                    l2 = l2.next
            ptr.next = tmp
            ptr = ptr.next
        return ans.next
```
Very simple linked list operation.
