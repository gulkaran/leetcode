# House Robber II

[https://leetcode.com/problems/house-robber-ii](https://leetcode.com/problems/house-robber-ii)

Use the solution from **House Robber** and run it on the arrays excluding $h_0$ and $h_n$

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        # nums = [1,2,2,3,5,1]
        # if you are i = 0, you cannot rob house n - 1

        if len(nums) == 1:
            return nums[0]
        
        def house_robber(nums):
            n = len(nums)
            opt = [0] * n
            opt[n - 1] = nums[n - 1]
            opt[n - 2] = nums[n - 2]

            for i in range(n - 3, -1, -1):
                opt[i] = nums[i] + max(opt[i + 2: n])
            
            return max(opt)

        return max(nums[0], house_robber(nums[1:]), house_robber(nums[:-1]))
```