# Word Search

[https://leetcode.com/problems/word-search](https://leetcode.com/problems/word-search)

We remove the node from the path since it can be used later on in the word. Also that creates the backtracking portion of the algorithm. We search in all 4 directions. The time complexity is $O(m\cdot 4^n)$ where $n$ is the len(word). 

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        
        m_rows = len(board)
        n_cols = len(board[0])

        path = set()

        def dfs(row, col, i):
            if i == len(word):
                return True
            
            if (0 > row or row >= m_rows or 0 > col or col >= n_cols or
                word[i] != board[row][col] or (row, col) in path):
                return False
            
            path.add((row, col))

            res = ( dfs(row + 1, col, i + 1) or 
                    dfs(row - 1, col, i + 1) or
                    dfs(row, col + 1, i + 1) or
                    dfs(row, col - 1, i + 1))
            
            path.remove((row, col))
            return res
        
        for row in range(m_rows):
            for col in range(n_cols):
                if dfs(row, col, 0):
                    return True

        return False
```