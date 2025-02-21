# Binary Tree Right Side View

[https://leetcode.com/problems/binary-tree-right-side-view/](https://leetcode.com/problems/binary-tree-right-side-view/description/)

BFS solution (similar to rotting oranges solution)

```python
from collections import deque

class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        view = []
        
        queue = deque()
        queue.append(root)

        while queue:
            lenq = len(queue)
            for i in range(lenq):
                node = queue.popleft()

                if i == lenq - 1:
                    view.append(node.val)
            
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            
        return view
```