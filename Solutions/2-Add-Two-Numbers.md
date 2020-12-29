# 2. Add Two Numbers

You are given two non-empty linked lists representing two **non-negative** integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Example 1:
![demo](/src/addtwonumber1.jpg)
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

## Example 2:
```
Input: l1 = [0], l2 = [0]
Output: [0]
```

## Example 3:
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

## Constraints:
- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

# Solution
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carry = 0
        ans = ListNode()
        ptr = ans
        while l1 or l2 or carry:
            if l1 == l2 == None:
                ptr.val = carry
                break
            elif not l1:
                ptr.val, carry = (carry + l2.val) % 10, (carry + l2.val) // 10
                if l2.next or carry:
                    ptr.next = ListNode()
                    ptr, l2 = ptr.next, l2.next
                else:
                    break
            elif not l2:
                ptr.val, carry = (carry + l1.val) % 10, (carry + l1.val) // 10
                if l1.next or carry:
                    ptr.next = ListNode()
                    ptr, l1 = ptr.next, l1.next
                else:
                    break
            else:
                ptr.val, carry = (carry + l1.val + l2.val) % 10, (carry + l1.val + l2.val) // 10
                if l1.next or l2.next or carry:
                    ptr.next = ListNode()
                    ptr, l1, l2 = ptr.next, l1.next, l2.next
                else:
                    break
        return ans
```
Basic simulation of mathematical plus '+' on two positive integers.

It also works if you convert them into integers first and convert back.
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        num1, num2 = '', ''
        while l1:
            num1, l1 = num1 + str(l1.val), l1.next
        while l2:
            num2, l2 = num2 + str(l2.val), l2.next
        num1, num2 = int(str(num1[::-1])), int(str(num2[::-1]))
        ans_num = num1 + num2
        ans = ListNode()
        ptr = ans
        while ans_num:
            ptr.val, ans_num = ans_num % 10, ans_num // 10
            if ans_num: 
                ptr.next = ListNode()
                ptr = ptr.next
        return ans
```
But that defeats the purpose of this problem.
