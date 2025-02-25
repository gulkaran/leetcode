# Unique Paths

[https://leetcode.com/problems/unique-paths/](https://leetcode.com/problems/unique-paths/)

We can notice that $OPT[i][j] = OPT[i +1][j] + OPT[i][j+1]$.

- essentially we can compute a current cells number of unique paths by checking how many unique paths are to the right and bottom of it (subproblems we have already solved!). From here, it has down + right unique choices to take.

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        
        opt = [[0] * n for _ in range(m)]  
        opt[m - 1][n - 1] = 1

        for row in range(m - 1, -1, -1): 
            for col in range(n - 1, -1, -1):  
                if (row, col) == (m - 1, n - 1):
                    continue
                
                right = opt[row][col + 1] if col + 1 < n else 0
                down = opt[row + 1][col] if row + 1 < m else 0

                opt[row][col] = right + down

        return opt[0][0]

```