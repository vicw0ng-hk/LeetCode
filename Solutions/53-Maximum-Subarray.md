# 53. Maximum Subarray

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

**Follow up**: If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.

## Example 1:
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Example 2:
```
Input: nums = [1]
Output: 1
```

## Example 3:
```
Input: nums = [0]
Output: 0
```

## Example 4:
```
Input: nums = [-1]
Output: -1
```

## Example 5:
```
Input: nums = [-2147483647]
Output: -2147483647
```

## Constraints:
- <code>1 <= nums.length <= 2 * 10<sup>4</sup></code>
- <code>2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1</code>

# Solution
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        ans, _sum = float('-inf'), float('-inf')
        for i in range(len(nums)):
            _sum = max(nums[i], _sum+nums[i])
            ans = max(ans, _sum)
        return ans
```
The `O(n)` solution. Also, the divide and conquer solution:
```python
class Solution:
    def maxCrossingSum(self, nums: List[int], left: int, mid: int, right: int) -> int:
        _sum, max_left_sum = 0, float('-inf')
        for i in range(mid, left-1, -1):
            _sum += nums[i]
            max_left_sum = max(max_left_sum, _sum)
        _sum, max_right_sum = 0, float('-inf')
        for i in range(mid+1, right+1):
            _sum += nums[i]
            max_right_sum = max(max_right_sum, _sum)
        return max_left_sum + max_right_sum
    def maxSubArraySum(self, nums: List[int], left: int, right: int) -> int:
        if left == right:
            return nums[left]
        mid = (left + right) // 2
        return max(self.maxSubArraySum(nums, left, mid), 
                   self.maxSubArraySum(nums, mid+1, right), 
                   self.maxCrossingSum(nums, left, mid, right))
    def maxSubArray(self, nums: List[int]) -> int:
        return self.maxSubArraySum(nums, 0, len(nums)-1)
```
Divide the array into two halves. Return the maximum of
- Maximum subarray sum in left half,
- Maximum subarray sum in right half,
- Maximum subarray sum such that the subarray crosses the midpoint.
