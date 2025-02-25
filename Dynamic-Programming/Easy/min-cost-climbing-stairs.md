# Min Cost Climbing Stairs

[https://leetcode.com/problems/min-cost-climbing-stairs/](https://leetcode.com/problems/min-cost-climbing-stairs/)

We see that this problem can be defined by subproblems and have the optimal solution be related (recursively) to those subproblems. Our base cases are clear

- the last two elements, the minimum cost to get up the stairs is the cost of those elements

We’ll notice that the optimal solution is $OPT[i] = cost[i] + min(OPT[i + 1], OPT[i + 2])$ since we can either move 1 or 2 steps. We could easily represent this as a recurrence relation and complete it with memoization, however, we take a **bottom-up** dynamic programming approach.

Finally, our return statement has the same logic of choosing the index 0 or 1 which minimizes the cost of the path up. 

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        n = len(cost)
        opt = [0] * n
        opt[n - 1] = cost[n - 1]
        opt[n - 2] = cost[n - 2]

        for i in range(n - 3, -1, -1):
            opt[i] = min(opt[i + 1], opt[i + 2]) + cost[i]
        
        return min(opt[0], opt[1])
```

Note: we can remove the extra memory of $OPT[]$ and compute everything in $cost[]$, however, to keep consistent and relate it to  what I’m learning in COMPSCI 3AC3 @ McMaster, I won’t omit it for understanding purposes.