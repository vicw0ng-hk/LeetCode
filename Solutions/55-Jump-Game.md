# 55. Jump Game

Given an array of non-negative integers `nums`, you are initially positioned at the **first index** of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

## Example 1:
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## Example 2:
```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

## Constraints:
- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>0 <= nums[i] <= 10<sup>5</sup></code>

# Solution
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        max_reachable, actually_reached = 0, 0
        for i in range(len(nums)-1):
            max_reachable = max(max_reachable, i+nums[i])
            if i == actually_reached:
                if max_reachable > actually_reached:
                    actually_reached = max_reachable
                else:
                    return False
        return True
```
Just be greedy. 
