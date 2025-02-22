# Surrounded Regions

[https://leetcode.com/problems/surrounded-regions](https://leetcode.com/problems/surrounded-regions/description/)

Most likely not the most optimal solution but still runs in $O(m \cdot n)$ time. Didn’t want a solution for this, did it during a mock interview. 

**My Intuition**

1. Find the ***valid*** regions
    1. we can ignore the border elements when we search for regions since any “O” on the border cannot not be *surrounded*
    2. valid region — define this as any region with no “O”s on the border 
2. Alter the board of any valid region

```python
from collections import deque

class Solution:
    def solve(self, board: List[List[str]]) -> None:
        
        m_rows = len(board)
        n_cols = len(board[0])
        seen = set()

        def find_region(row, col):
            queue = deque()
            queue.append((row, col))
            seen.add((row, col))
            valid = True
            o_coords = []

            directions = [(1, 0), (0, 1), (-1, 0), (0, -1)]

            while queue:
                r, c = queue.popleft()
                o_coords.append((r, c))

                for dir_r, dir_c in directions:
                    dr, dc = r + dir_r, c + dir_c
                    
                    if (0 <= dr < m_rows and 0 <= dc < n_cols and 
                        board[dr][dc] == "O" and (dr, dc) not in seen):
                        queue.append((dr, dc))
                        seen.add((dr, dc))

                        # on border (can't be valid region)
                        if (0 == dr or dr == m_rows - 1 or 0 == dc or dc == n_cols - 1):
                            valid = False

            return valid, o_coords

        
        for row in range(1, m_rows - 1):
            for col in range(1, n_cols - 1):
                if board[row][col] == "O" and (row, col) not in seen:
                    valid, output = find_region(row, col)

                    if valid:
                        for r, c in output:
                            board[r][c] = "X"

```