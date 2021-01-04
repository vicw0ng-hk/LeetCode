# 45. Jump Game II

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

## Example 1:
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## Example 2:
```
Input: nums = [2,3,0,1,4]
Output: 2
```

## Constraints:
- <code>1 <= nums.length <= 3 * 10<sup>4</sup></code>
- <code>0 <= nums[i] <= 10<sup>5</sup></code>

# Solution
```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        ans = 0
        max_reachable, actually_reached = 0, 0
        for i in range(len(nums)-1):
            max_reachable = max(max_reachable, i+nums[i])
            if i == actually_reached:
                ans += 1
                actually_reached = max_reachable
        return ans
```
Always keep track of the range `n` steps could reach. Be greedy.
