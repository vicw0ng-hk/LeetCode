# 81. Search in Rotated Sorted Array II

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true` *if* `target` *is in* `nums`, *or* `false` *if it is not in* `nums`.

## Example 1:
```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

## Example 2:
```
Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

## Constraints:
- `1 <= nums.length <= 5000`
- <code>-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup></code>
- `nums` is guaranteed to be rotated at some pivot.
- <code>-10<sup>4</sup> <= target <= 10<sup>4</sup></code>

**Follow up**: This problem is the same as [Search in Rotated Sorted Array](Solutions/33-Search-in-Rotated-Sorted-Array.md), where `nums` may contain **duplicates**. Would this affect the runtime complexity? How and why?

# Solution
```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        if len(nums) < 3:
            return target in nums
        start, end = 0, len(nums) - 1
        while start <= end:
            mid = (start + end) >> 1
            if target in [nums[start], nums[mid], nums[end]]:
                return True
            if nums[start] == nums[mid]:
                start += 1
            elif nums[start] <= nums[mid] and nums[start] > target:
                start = mid + 1
            elif nums[start] > nums[mid] and nums[start] <= target:
                end = mid - 1
            elif nums[mid] < target:
                start = mid + 1
            else:
                end = mid - 1
        return False
```
Use binary search. If `nums[start] <= nums[mid]` XOR `nums[start] <= target` is true, then target is not in the same half where rotation cut is. Time complexity: worse case `O(n)`, best case `O(logn)`.
