# Same Tree

[https://leetcode.com/problems/same-tree](https://leetcode.com/problems/same-tree/description/)

```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        
        # base case, both are null
        if not p and not q:
            return True

        # false case where 2 nodes are not equal
        if (p and not q) or (q and not p) or p.val != q.val:
            return False

        # check both halves
        return self.isSameTree(p.right, q.right) and self.isSameTree(p.left, q.left)
```