# Container With Most Water

[https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)

### Brute Force

Iterate through the entire heights array and compute the area for each possibility - $O(n^2)$

- you’ll notice that if we start at opposite ends, that is the largest length we can get
- the largest height is also bottlenecked by the smaller height

### Optimal 2 Pointer Approach

- Start at opposite ends
- Calculate the height
- Change the pointer of the bottlenecking height, ensure we are keeping the larger height

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        maxArea = 0

        while l < r:
            # compute the height
            area = min(height[l], height[r]) * (r-l)
            maxArea = max(maxArea, area)

            # inc/dec the bottleneck
            if height[l] < height[r]:
                l += 1
            else: 
                r -= 1

        return maxArea
```