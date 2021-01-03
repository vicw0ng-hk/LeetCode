# 35. Search Insert Position

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

## Example 1:
```
Input: nums = [1,3,5,6], target = 5
Output: 2
```

## Example 2:
```
Input: nums = [1,3,5,6], target = 2
Output: 1
```

## Example 3:
```
Input: nums = [1,3,5,6], target = 7
Output: 4
```

## Example 4:
```
Input: nums = [1,3,5,6], target = 0
Output: 0
```

## Example 5:
```
Input: nums = [1], target = 0
Output: 0
```

## Constraints:
- <code>1 <= nums.length <= 10<sup>4</sup></code>
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `nums` contains **distinct** values sorted in **ascending** order.
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

# Solution
```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        if target < nums[0]:
            return 0
        if target > nums[-1]:
            return len(nums)
        left, right = 0, len(nums) - 1
        while left <= right:
            print(left, right)
            mid = (left + right + 1) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] < target:
                left = mid + 1
            if nums[mid] > target:
                right = mid - 1
        return left
```
Binary Search.
