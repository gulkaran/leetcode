# Spiral Matrix

Just need to account for 4 boundaries and update them accordingly for each pass.

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix:
            return []
        
        top = 0
        left = 0
        bottom = len(matrix)
        right = len(matrix[0])

        result = []

        while left < right and top < bottom:
            # top pass
            for col in range(left, right):
                result.append(matrix[top][col])
            
            top += 1

            # right pass
            for row in range(top, bottom):
                result.append(matrix[row][right - 1])
            
            right -= 1

            if not (left < right and top < bottom):
                break

            # bottom pass
            for col in range(right - 1, left - 1, -1):
                result.append(matrix[bottom - 1][col])

            bottom -= 1
            
            # left pass
            for row in range(bottom - 1, top - 1, -1):
                result.append(matrix[row][left])
            
            left += 1

        return result
```