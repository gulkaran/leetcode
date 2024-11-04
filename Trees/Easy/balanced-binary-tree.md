# Balanced Binary Tree

[https://leetcode.com/problems/balanced-binary-tree](https://leetcode.com/problems/balanced-binary-tree)

We want to start at the bottom layer instead of the root to avoid doing the same calculation over and over again. The naive approach would be to repeatedly calculate the height of the subtrees and compare them, and then do this for *every* node in the tree causing it run in $O(n^2)$ time.

Instead, we start the bottom nodes and work ourselves up.

```python
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        
        def dfs(root):
            if not root:
                return [True, 0] # [balanced_so_far, height]
            
            # get to the bottom most layer of the tree
            left = dfs(root.left)
            right = dfs(root.right)

            # left + right subtrees currently balanced + height requirement
            balanced = left[0] and right[0] and abs(left[1] - right[1]) <= 1

            return [balanced, 1 + max(left[1], right[1])]

        return dfs(root)[0]

```