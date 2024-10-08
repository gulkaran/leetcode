# Search a 2d Matrix

[https://leetcode.com/problems/search-a-2d-matrix/](https://leetcode.com/problems/search-a-2d-matrix/)

### Problem

Given a $m \times n$ integer matrix, there are two properties

- every row is sorted in ascending order
- the first integer of each row is greater than the last integer of the previous row

Given a $target$ integer, return $True$ if the $target$ is found, $false$ otherwise.

### Solution

The solution needs to be $O(\log{m \cdot n})$. We know we can use binary search since the rows are sorted in ascending order. This is already a $O(\log{m})$ operation. We can find **which row** to search by utilizing the second property of the matrix where the first integer of a row is larger than the last of the previous row. 

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        # do binary search based on where the element would be

        for row in matrix:
			      # search this row if the target is smaller than the last element
            if target <= row[-1]:

                l, r = 0, len(row) - 1
                while l <= r:
                    mid = (r + l) // 2
                    if target == row[mid]:
                        return True
                    elif target > row[mid]:
                        l = mid + 1
                    else:
                        r = mid - 1
        
        return False
```