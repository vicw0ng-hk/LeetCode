# 25. Reverse Nodes in k-Group

Given a linked list, reverse the nodes of a linked list *k* at a time and return its modified list.

*k* is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of *k* then left-out nodes, in the end, should remain as it is.

**Follow up**:
- Could you solve the problem in `O(1)` extra memory space?
- You may not alter the values in the list's nodes, only nodes itself may be changed.

## Example 1:
![swap_ex1.jpg](/src/swap_ex1.jpg)
```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

## Example 2:
![swap_ex2.jpg](/src/swap_ex2.jpg)
```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

## Example 3:
```
Input: head = [1,2,3,4,5], k = 1
Output: [1,2,3,4,5]
```

## Example 4:
```
Input: head = [1], k = 1
Output: [1]
```

## Constraints:

The number of nodes in the list is in the range `sz`.
- `1 <= sz <= 5000`
- `0 <= Node.val <= 1000`
- `1 <= k <= sz`

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseK(self, ptr1: ListNode, ptr2: ListNode, k: int) -> ListNode:
        if k == 1:
            return ptr1
        if k == 2:
            tmp = ptr1.next
            tmp.next = ptr2.next
            ptr1.next = ptr2
            ptr2.next = tmp
            return ptr1
        else:
            tmp1 = ptr1.next
            tmp2 = ptr1.next.next
            tmp1.next = ptr2.next
            ptr1.next = tmp2
            ptr2.next = tmp1
            return self.reverseK(ptr1, ptr2, k-1)
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        flag = 0
        ans = ListNode()
        ans.next = head
        ptr1, ptr2 = ans, ans
        while True:
            for i in range(k):
                if ptr2.next == None:
                    flag = 1
                    break
                ptr2 = ptr2.next
            if flag == 1: 
                break
            ptr1 = self.reverseK(ptr1, ptr2, k)
            for i in range(k):
                ptr1 = ptr1.next
            ptr2 = ptr1
        return ans.next
```
Somewhat complicated linked list operation. 
