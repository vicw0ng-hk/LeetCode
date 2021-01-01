# 23. Merge k Sorted Lists

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

*Merge all the linked-lists into one sorted linked-list and return it*.

## Example 1:
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

## Example 2:
```
Input: lists = []
Output: []
```

## Example 3:
```
Input: lists = [[]]
Output: []
```

## Constraints:
- `k == lists.length`
- `0 <= k <= 10^4`
- `0 <= lists[i].length <= 500`
- `-10^4 <= lists[i][j] <= 10^4`
- `lists[i]` is sorted in **ascending order**.
- The sum of `lists[i].length` won't exceed `10^4`.

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
import heapq

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        ref = []
        ans = ListNode()
        ptr = ans
        for i in range(len(lists)):
            if lists[i] != None:
                ref.append((lists[i].val, i))
        heapq.heapify(ref)
        while ref:
            tmp = heapq.heappop(ref)
            tmp_node = ListNode(tmp[0])
            lists[tmp[1]] = lists[tmp[1]].next
            if lists[tmp[1]] != None:
                heapq.heappush(ref, (lists[tmp[1]].val, tmp[1]))
            ptr.next = tmp_node
            ptr = ptr.next
        return ans.next
```
Use a priority queue to store a reference of (`list's first node value`, `list index`): O(nlogk)

Or alternatively, use divide and conquer: O(nlogk)
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
        while l1 and l2:
            if l1.val <= l2.val:
                ptr.next = l1
                l1 = l1.next
            else:
                ptr.next = l2
                l2 = l1
                l1 = ptr.next.next
            ptr = ptr.next
        if not l1:
            ptr.next=l2
        else:
            ptr.next=l1
        return ans.next
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        count = 1
        while count < len(lists):
            for i in range(0, len(lists) - count, count * 2):
                lists[i] = self.mergeTwoLists(lists[i], lists[i+count])
            count *= 2
        return lists[0] if lists else None
```
