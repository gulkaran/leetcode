# All Nodes Distance K in Binary Tree

[https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

Convert to a graph problem since we also need to travel upwards through the target’s parent. Create an adj list and do bfs tracking distances! 

```python
from collections import deque, defaultdict

class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
        queue = deque()
        adj = defaultdict(list)
        queue.append(root)
        
        # build adjaceny list (convert this to graph problem since we need 
        # the root parent)
        while queue:
            node = queue.popleft()

            if node.left:
                queue.append(node.left)
                
                adj[node.val].append(node.left.val)
                adj[node.left.val].append(node.val)

            
            if node.right:
                queue.append(node.right)

                adj[node.val].append(node.right.val)
                adj[node.right.val].append(node.val)

        # now do simple bfs tracking distances until dist == k
        queue.append((target.val, 0))
        seen = set()
        seen.add(target.val)
        res = []

        while queue:
            node, dist = queue.popleft()

            if k == dist:
                res.append(node)

            else:
                for n in adj[node]:
                    if n not in seen:
                        queue.append((n, dist + 1))
                        seen.add(n)

        return res
```