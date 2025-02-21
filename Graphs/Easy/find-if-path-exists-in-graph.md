# Find if Path Exists in Graph

[https://leetcode.com/problems/find-if-path-exists-in-graph](https://leetcode.com/problems/find-if-path-exists-in-graph)

Create the adj list and then do **DFS** from the source node. If the path exists, it will eventually show up in the stack.

```python
from collections import defaultdict

class Solution:
    def validPath(self, n: int, edges: List[List[int]], source: int, destination: int) -> bool:
        
        # create adj list then dfs
        adj = defaultdict(list)

        for u, v in edges:
            adj[u].append(v)
            adj[v].append(u)

        marked = set()
        stack = [source]
        marked.add(source)
        
        while stack:
            v = stack.pop()
            if v == destination:
                return True

            for w in adj[v]:
                if w not in marked:
                    stack.append(w)
                    marked.add(w)
        
        return False

```