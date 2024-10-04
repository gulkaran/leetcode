# Number of Islands

[https://leetcode.com/problems/number-of-islands](https://leetcode.com/problems/number-of-islands/description/)/

Simple BFS solution to visit neighbouring “1”s in the grid and mark them. If we encounter a new “1” in the grid that hasn’t been visited, we know its a new island and check its neighbours as well.

```python
import collections

class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:

        marked = set()
        islands = 0

        if not grid:
            return islands

        num_of_rows = len(grid)
        num_of_cols = len(grid[0])

        def bfs(row, col):
            queue = deque()
            marked.add((row, col))

            queue.append((row, col))
            while queue: 
                (row, col) = queue.popleft()
                
                directions = [[1, 0], [-1, 0], [0, 1], [0, -1]]
                
                for dr in directions:
                    r, c = row + dr[0], col + dr[1]

                    if (0 <= r <= num_of_rows-1 and
                        0 <= c <= num_of_cols-1 and
                        (r, c) not in marked and
                        grid[r][c] == "1"):

                        marked.add((r,c))
                        queue.append((r,c))

        for row in range(num_of_rows):
            for col in range(num_of_cols):

                if grid[row][col] == "1" and (row, col) not in marked:
                    bfs(row, col)
                    islands += 1

        return islands
        
```

Fun fact I got this question asked in my Scotiabank interview :)