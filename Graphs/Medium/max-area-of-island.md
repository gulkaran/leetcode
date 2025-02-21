# Max Area of Island

[https://leetcode.com/problems/max-area-of-island/](https://leetcode.com/problems/max-area-of-island/)

Similar question to number of islands, but here we count the area as how many times we pop from the queue.

```python
from collections import deque

class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        if not grid:
            return 0

        m_rows = len(grid)
        n_cols = len(grid[0])
        max_area = 0
        marked = set()

        def bfs(row, col):
            queue = deque()
            queue.append((row, col))
            marked.add((row, col))
            area = 0

            dirs = [(1, 0), (0, 1), (0, -1), (-1, 0)]
            while queue: 
                r, c = queue.popleft()
                area += 1

                for d in dirs:
                    dr, dc = r + d[0], c + d[1]

                    if (0 <= dr < m_rows and
                        0 <= dc < n_cols and
                        grid[dr][dc] == 1 and
                        (dr, dc) not in marked): 
                        queue.append((dr, dc))
                        marked.add((dr, dc))

            return area

        for row in range(m_rows):
            for col in range(n_cols):
                if grid[row][col] == 1 and (row, col) not in marked:
                    area = bfs(row, col)
                    max_area = max(max_area, area)
        
        return max_area
        

```