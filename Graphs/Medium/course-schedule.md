# Course Schedule

[https://leetcode.com/problems/course-schedule/](https://leetcode.com/problems/course-schedule/)

Based on the idea of cycle detection. 

- Create the adj list
- Recursive dfs where we add $v$ to the stack
    - if we somehow see $v$ again checking $w$’s adj list then we know there is a cycle

```python
from collections import defaultdict

class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        if not prerequisites:
            return True

        adj = defaultdict(list)

        for u, v in prerequisites:
            adj[v].append(u)
        
        seen = set()
        stack = set()
        has_cycle = False

        def dfs(v):
            nonlocal has_cycle

            seen.add(v)
            stack.add(v)

            for w in adj[v]:
                if has_cycle:
                    return

                if w in stack:
                    has_cycle = True

                elif w not in seen:
                    dfs(w)
            
            stack.remove(v)

        for i in range(numCourses):
            if i not in seen:
                dfs(i)

        return not has_cycle
```