# House Robber

[https://leetcode.com/problems/house-robber/](https://leetcode.com/problems/house-robber/)

We ❤️ **bottom-up** dynamic programming! 

Notice the relation of how the optimal cost is the value of the house + the optimal value of any path atleast 1 house down ($i + 2)$. So if we start from the end and get the base cases of the last two elements, we can continue to define the smaller subproblems and gradually compute the optimal value for our initial problem.

### **Example**

Consider the example $nums=[2, 7, 9, 13, 1]$

**Base Case**

For houses $n-1$ and $n-2$, they cannot jump any more houses so the optimal path from there is the house’s value itself.

For house $i$, its optimal value is its own value + the maximum path from $i + 2$ onwards. For example, the house $i=0$ with value 2 can choose the optimal path from $i=2\to n-1$. 

$OPT[]=[0,20,10,13,1]$ in this case, so it’ll compute $OPT[0] = 2 + max([10,13,1])$ which results in $OPT[0] = 15$

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # opt[i] = nums[i] + max(opt[i + 2 : n])

        # nums = [2,7,9,13,1]
        # loop    i   ->   n

        # opt[0] = opt[2 : n]

        n = len(nums)
        opt = [0] * n
        opt[n - 1] = nums[n - 1]
        opt[n - 2] = nums[n - 2]

        for i in range(n - 3, -1, -1):
            opt[i] = nums[i] + max(opt[i + 2 : n])

        return max(opt)
```