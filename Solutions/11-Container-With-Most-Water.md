# 11. Container With Most Water

Given n non-negative integers <code>a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub></code>, where each represents a point at coordinate <code>(i, a<sub>i</sub>)</code>. `n` vertical lines are drawn such that the two endpoints of the line `i` is at <code>(i, a<sub>i</sub>)</code> and `(i, 0)`. Find two lines, which, together with the x-axis forms a container, such that the container contains the most water.

**Notice** that you may not slant the container.

## Example 1:

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

## Example 2:
```
Input: height = [1,1]
Output: 1
```

## Example 3:
```
Input: height = [4,3,2,1,4]
Output: 16
```

## Example 4:
```
Input: height = [1,2,1]
Output: 2
```

## Constraints:
- `n = height.length`
- <code>2 <= n <= 3 * 10<sup>4</sup></code>
- <code>0 <= height[i] <= 3 * 10<sup>4</sup></code>

# Solution
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right, max_area = 0, len(height) - 1, 0
        while left < right:
            max_area = max(max_area, min(height[left], height[right]) * (right - left))
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return max_area
```
Use a two pointer model. Notice the conditions for changing `left` and `right` value.
