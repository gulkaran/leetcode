# Rotting Oranges

[https://leetcode.com/problems/rotting-oranges/](https://leetcode.com/problems/rotting-oranges/)

A minute passes after every rotten orange in our queue is popped.

Remember to account for:

- **multiple** rotten oranges rotting fresh oranges (this is why we iterate over the length of queue)
- if a fresh orange can’t be reached (rottened) by a rotten orange (checking if fresh == 0 in our return statement)

```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        
        if not grid:
            return -1

        rows = len(grid)
        cols = len(grid[0])
        minutes = 0
        fresh = 0
        queue = deque()

        for row in range(rows):
            for col in range(cols):
                if grid[row][col] == 1:
                    fresh += 1
                elif grid[row][col] == 2:
                    queue.append((row, col))

        dirs = [(1,0),(0,1),(-1,0),(0,-1)]
        while queue and fresh > 0:

            for _ in range(len(queue)):
                r, c = queue.popleft()

                for dr, dc in dirs:
                    x, y = r + dr, c + dc

                    if (0 <= x < rows and
                        0 <= y < cols and
                        grid[x][y] == 1):
                        grid[x][y] = 2
                        queue.append((x,y))
                        fresh -= 1
            
            minutes += 1
        

        return minutes if fresh == 0 else -1
```