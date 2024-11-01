# Maximum Depth of Binary Tree

[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)

Memorized from my COMPSCI 2C03 notes haha.

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        return max(self.maxDepth(root.right), self.maxDepth(root.left)) + 1
```

This function recursively calls height until we reach the traversal of the null nodes. ‘height()’ will return a value, so that is used in the outer recursive call as a value as seen below.

![example.png](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa97a750a-e62b-4c5e-8254-61386573f4c2%2Fc7e5bdb3-7109-4395-8c7d-98e0bf5eb313%2FScreenshot_2024-10-29_at_8.54.34_PM.png?table=block&id=12f407fa-a245-8013-af57-d1dd6b600dbd&spaceId=a97a750a-e62b-4c5e-8254-61386573f4c2&width=2000&userId=9662b736-eaf6-4a2e-967f-10faf2d70a83&cache=v2)
