# 42. Trapping Rain Water

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Example 1:
![rainwatertrap.png](/src/rainwatertrap.png)
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

## Example 2:
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

## Constraints:
- `n == height.length`
- <code>0 <= n <= 3 * 10<sup>4</sup></code>
- <code>0 <= height[i] <= 10<sup>5</sup></code>

# Solution
```python
class Solution:
    def trap(self, height: List[int]) -> int:
        ans = 0
        left, right = 0, len(height) - 1
        left_max, right_max = 0, 0
        while left < right:
            left_max, right_max = max(left_max, height[left]), max(right_max, height[right])
            if left_max < right_max:
                ans += max(0, left_max - height[left])
                left += 1
            else:
                ans += max(0, right_max - height[right])
                right -= 1
        return ans
```
Use two pointers and record max heights from left and right. 
