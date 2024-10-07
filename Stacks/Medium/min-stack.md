# Min Stack

[https://leetcode.com/problems/min-stack/](https://leetcode.com/problems/min-stack/)

We want every ‘node’ in the stack to keep track of the minimum value. So if we push -2, 0 and -3, the first 2 nodes will have -2 tracked as the minimum value. The -3 node updates the minimum value as -3. 

We could create a new MinNode structure that tracks it, however, an easier method is to just keep track of an minStack array that tracks the same information.

- $stack = [-2,0,-3]$
- $minStack = [-2,-2,-3]$

```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        minVal = min(val, self.minStack[-1] if self.minStack else val)
        self.minStack.append(minVal)
        
    def pop(self) -> None:
        self.stack.pop()
        self.minStack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
```