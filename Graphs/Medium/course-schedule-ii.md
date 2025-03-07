# Course Schedule II

[https://leetcode.com/problems/course-schedule-ii/](https://leetcode.com/problems/course-schedule-ii/)

Topological sort

- DFS post order traversal (when dfs call is done)
- reverse that list ^^^

```python
from collections import defaultdict

class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        
        adj = defaultdict(list) # { : []}

        for u, v in prerequisites:
           adj[v].append(u)

        marked = set()
        stack = set()
        has_cycle = False
        output = []

        def dfs(v):
            nonlocal has_cycle

            marked.add(v)
            stack.add(v)

            for w in adj[v]:
                if has_cycle:
                    return
                
                if w in stack:
                    has_cycle = True

                elif w not in marked:
                    dfs(w)

            stack.remove(v)
            output.append(v)

        for i in range(numCourses):
            if i not in marked:
                dfs(i)
        
        return [] if has_cycle else output[::-1]
```

Note: could remove the reversal of the list and make adj list $u\to v$ instead but just did it this way to keep consistent with what I learned in 2C03 @ McMaster