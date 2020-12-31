# 16. 3Sum Closest

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

## Example 1:
```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## Constraints:
- `3 <= nums.length <= 10^3`
- `-10^3 <= nums[i] <= 10^3`
- `-10^4 <= target <= 10^4`

# Solution
```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        diff = float('inf')
        for left in range(len(nums) - 2):
            mid, right = left + 1, len(nums) - 1
            while mid < right:
                _sum = nums[left] + nums[mid] + nums[right]
                if abs(_sum - target) < abs(diff):
                    diff = _sum - target
                if _sum < target:
                    mid += 1
                elif _sum > target:
                    right -= 1
                else:
                    return target
        return diff + target
```
Similar to [3Sum](/Solutions/15-3Sum.md), but with a specified target (instead of 0) and a difference to minimize. 
