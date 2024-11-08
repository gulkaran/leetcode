# Subtree of Another Tree

[https://leetcode.com/problems/subtree-of-another-tree](https://leetcode.com/problems/subtree-of-another-tree)

We simply use our previous solution for the **Same Tree** problem and implement it here. 

```python
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        if not root:
            return False

        if not subRoot:
            return True
        
        if self.sameTree(root, subRoot):
            return True

        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

    def sameTree(self, p, q):
        if not p and not q:
            return True
        
        if (not p and q) or (not q and p) or (p.val != q.val):
            return False
        
        return self.sameTree(p.left, q.left) and self.sameTree(p.right, q.right)
```