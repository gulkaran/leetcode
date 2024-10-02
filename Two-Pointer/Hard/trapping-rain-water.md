# Trapping Rain Water 

https://leetcode.com/problems/trapping-rain-water/

This question is a doozy, but it uses a two pointer approach based on the intuition that you can calculate how much rain can be trapped at any position $i$ if you know the maximum left and right heights. This is because you can store potentially up to the max heights, bottlenecked by the lower max height.

### Example

![example.png](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa97a750a-e62b-4c5e-8254-61386573f4c2%2F46fad961-4893-4848-8201-70bf5408a10c%2FScreenshot_2024-03-25_at_10.35.42_PM.png?table=block&id=be001ede-69e3-489a-b67a-4b072c5384b5&spaceId=a97a750a-e62b-4c5e-8254-61386573f4c2&width=2000&userId=9662b736-eaf6-4a2e-967f-10faf2d70a83&cache=v2)

We can use an $O(n)$ memory solution where we store the max right and max left in arrays, however, noticing this small trick will net us an $O(1)$ memory solution.

### Optimal Solution

- start with left and right pointers (l = 0, r = len(height) - 1)
- have starting maxLeft and maxRight variables
- move the pointer which has the **minimum** value
- since we’ve moved the pointer with the lower value, we are allowed to calculate the rain that position can capture using the max value of the pointer we moved, as the bottleneck.
  - but how? what about the other max value? Since we moved the pointer with the **lower** value, we know the OTHER pointer was larger (or same) so this position’s calculated rain can only be **bottlenecked** by the pointer we just moved.
- notes:
  - imagine a left staircase 📶, as we update the lMax, we don’t need to update the rain counter as the rain would trickle off to the left of it. Our calculation of rain would yield us a negative number.
    - we still do the calculation in code for cleaner code but it always adds 0
  - key point is we move the side of the lower max value because we’re bottlenecked by that side!

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        l, r = 0, len(height)-1
        lMax, rMax = height[l], height[r]
        rain = 0

        while l < r:
            if lMax < rMax:
                l += 1
                lMax = max(lMax, height[l])
                rain += lMax - height[l]
            else:
                r -= 1
                rMax = max(rMax, height[r])
                rain += rMax - height[r]

        return rain
```

Note by updating the max values before calculating the rain, we ignore the possibility of negative heights and ignore checking that condition
