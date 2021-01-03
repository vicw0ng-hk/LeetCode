# 34. Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

**Follow up**: Could you write an algorithm with `O(log n)` runtime complexity?

## Example 1:
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

## Example 2:
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

## Example 3:
```
Input: nums = [], target = 0
Output: [-1,-1]
```

## Constraints:
- <code>0 <= nums.length <= 10<sup>5</sup></code>
- <code>-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup></code>
- `nums` is a non-decreasing array.
- <code>-10<sup>9</sup> <= target <= 10<sup>9</sup></code>

# Solution
```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        if not nums or target < nums[0] or target > nums[-1]:
            return [-1, -1]
        left_1, right_1 = 0, len(nums)
        while left_1 < right_1:
            mid_1 = (left_1 + right_1) // 2
            if nums[mid_1] >= target:
                right_1 = mid_1
            else:
                left_1 = mid_1 + 1
        if nums[left_1] != target:
            return [-1, -1]
        if nums[-1] == target:
            return [left_1, len(nums)-1]
        left_2, right_2 = left_1, len(nums)
        while left_2 < right_2:
            mid_2 = (left_2 + right_2 + 1) // 2
            if nums[mid_2] <= target:
                left_2 = mid_2
            else:
                right_2 = mid_2 - 1
        return [left_1, right_2]
```
Use 2 binary searches.
