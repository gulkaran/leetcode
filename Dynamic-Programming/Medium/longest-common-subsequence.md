# Longest Common Subsequence

[https://leetcode.com/problems/longest-common-subsequence](https://leetcode.com/problems/longest-common-subsequence)

We notice we have a choice for the optimal value for any 2 strings.

- if the starting character is the same between the 2 strings are equal, the longest subsequence must include that character so we can + 1 the optimal value of the two strings excluding that character. For example, the optimal value for (abc, aec) is simply the optimal value of (bc, ec) + 1

- for starting characters not equal, we have a choice from which we’ll simply take the largest value from. Consider the previous example
    1. (bc, c)
    2. (c, ec)

$\text{OPT}[i][j]=
\begin{cases}
1 + \text{OPT}[i + 1][j + 1] & \text{if str1[i] == str[j]} \\
\max(\text{OPT}[i+1][j], \text{OPT}[i][j+1]) & \text{otherwise}

\end{cases}$

Again we use **bottom-up** dynamic programming to solve the smallest subproblems first. From this approach, we know our return value is at $OPT[0][0]$

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        n = len(text1)
        m = len(text2)

        opt = [([0] * (m + 1)) for _ in range(n + 1)]

        for i in range(n - 1, -1, -1):
            for j in range(m - 1, -1, -1):

                if text1[i] == text2[j]: 
                    opt[i][j] = 1 + opt[i + 1][j + 1]
                else:
                    opt[i][j] = max(opt[i + 1][j], opt[i][j + 1])
        
        return opt[0][0]
```