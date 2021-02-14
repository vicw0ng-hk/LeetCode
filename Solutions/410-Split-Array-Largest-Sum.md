# 410. Split Array Largest Sum

Given an array `nums` which consists of non-negative integers and an integer `m`, you can split the array into `m` non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these `m` subarrays.

## Example 1:
```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

## Example 2:
```
Input: nums = [1,2,3,4,5], m = 2
Output: 9
```

## Example 3:
```
Input: nums = [1,4,4], m = 3
Output: 4
```

## Constraints:
- `1 <= nums.length <= 1000`
- <code>0 <= nums[i] <= 10<sup>6</sup></code>
- `1 <= m <= min(50, nums.length)`

# Solution
```python
class Solution:
    def greedySplit(self, nums: List[int], maxsum: int) -> int:
        total, ans = 0, 1
        for n in nums:
            total += n
            if total > maxsum:
                total = n
                ans += 1
        return ans
    def splitArray(self, nums: List[int], m: int) -> int:
        low = max(nums)
        high = sum(nums)
        while low < high:
            mid = (low + high) // 2
            if self.greedySplit(nums, mid) <= m:
                high = mid
            else:
                low = mid + 1
        return low
```
[Painter's Partition Problem](https://www.geeksforgeeks.org/painters-partition-problem-set-2/). Encountered in [COMP3250](https://www.cs.hku.hk/index.php/programmes/course-offered?infile=2020/comp3250.html 'COMP3250 Design and analysis of algorithms [Section 2B, 2020]') @ [HKU](https://hku.hk). 
