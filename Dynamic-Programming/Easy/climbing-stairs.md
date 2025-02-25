# Climbing Stairs

[https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)

We notice that the $OPT$ solution is based on the previous 2 subproblems. This is a **bottom-up** dynamic programming approach where $OPT[i] = OPT[i-1] + OPT[i-2]$

The intuition for this solution being fibonacci’s sequence is that for $n=4$, if we consider $n=3$, we’ll see that we can get from $3 \to 4$ by taking 1 step. For $n=2$, we can take 2 steps and get to $n=4$. So we can see the optimal solution is recursively related to its smaller subproblems.

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        opt = [0] * (n + 1)
        opt[0] = 1
        opt[1] = 1

        for i in range(2, n + 1):
            opt[i] = opt[i - 1] + opt[i - 2]
        
        return opt[n]
```

Note there is a way to not use extra memory in terms swapping variables but we will stick with this approach as it clearly explains the recurrence relation!