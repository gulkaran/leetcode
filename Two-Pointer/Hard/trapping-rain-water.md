# Trapping Rain Water <img align="right" height="50" src="https://upload.wikimedia.org/wikipedia/commons/8/8e/LeetCode_Logo_1.png"/>

This question is a doozy, but it uses a two pointer approach based on the intuition that you can calculate how much rain can be trapped at any position $i$ if you know the maximum left and right heights. This is because you can store potentially up to the max heights, bottlenecked by the lower max height.

### Example

![example.png](https://cdn.discordapp.com/attachments/925952083616735255/1227061224324464772/img.png?ex=662708d1&is=661493d1&hm=da54265774265af92886d9fbfd93be47b3902bb8b7710e2af299e874e6c1605c&)

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
