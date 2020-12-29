# 4. Median of Two Sorted Arrays

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return **the median** of the two sorted arrays.

**Follow up**: The overall run time complexity should be `O(log (m+n))`.

## Example 1:
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

## Example 2:
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

## Example 3:
```
Input: nums1 = [0,0], nums2 = [0,0]
Output: 0.00000
```

## Example 4:
```
Input: nums1 = [], nums2 = [1]
Output: 1.00000
```

## Example 5:
```
Input: nums1 = [2], nums2 = []
Output: 2.00000
```

## Constraints:
- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- <code>-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup></code>

# Solution
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        nums1_length, nums2_length = len(nums1), len(nums2)
        if nums1_length > nums2_length:
            return self.findMedianSortedArrays(nums2, nums1)
        low, high = 0, nums1_length
        while low <= high:
            cut1 = (low + high) // 2
            cut2 = (nums1_length + nums2_length) // 2 - cut1
            left1 = float('-inf') if cut1 == 0 else nums1[cut1-1]
            left2 = float('-inf') if cut2 == 0 else nums2[cut2-1]
            right1 = float('inf') if cut1 == nums1_length else nums1[cut1]
            right2 = float('inf') if cut2 == nums2_length else nums2[cut2]
            if left1 > right2: 
                high = cut1 - 1
            elif left2 > right1: 
                low = cut1 + 1
            else: 
                return min(right1, right2) if (nums1_length + nums2_length) % 2 else (max(left1, left2) + min(right1, right2)) / 2
```
The logic here is a bit complicated. The gist is to use binary search (O(log(n))) to find a position to 'cut' the shorter array, and since the two arrays are both sorted, the position to cut in the other array is also determined. Then we need to verify whether the left sides of both arrays are smaller than the right side of either array (a valid cut). 

Of course, this will also pass:
```python
import statistics

class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        return statistics.median(nums1 + nums2)
```
But that defeats the purpose of this problem. 

Also the to find the median of **one** array:
```python
def median(self, nums:List[int]) -> float:
    return (nums[(len(nums)-1)//2] + nums[(len(nums))//2]) / 2
```
