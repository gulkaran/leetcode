# Valid Sudoku

[https://leetcode.com/problems/valid-sudoku/](https://leetcode.com/problems/valid-sudoku/)

No real trick for this one, checking if value is in the row/col is just checking if its in a set

- checking within the 3x3 subsquares is as easy as dividing the row or col by 3 (int division)
- use a dictionary where the **key** is the index of the row → value is hashset

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        
        # key -> row or col or (parentRow, parentCol) index
        # val -> hashset for that row, col, parentSqaure
        rows = collections.defaultdict(set)
        cols = collections.defaultdict(set)
        squares = collections.defaultdict(set)

        for row in range(len(board)):
            for col in range(len(board[row])):

                cell = board[row][col]

                if (cell) == ".":
                    continue

								# checks if cell in any of the 3 hashsets
                if (cell in rows[row] or
                    cell in cols[col] or
                    cell in squares[ (row // 3, col // 3) ]):
                    return False

                rows[row].add(cell)
                cols[col].add(cell)
                squares[ (row // 3, col // 3) ].add(cell)

        return True
```