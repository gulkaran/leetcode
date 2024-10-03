# Valid Parentheses

https://leetcode.com/problems/valid-parentheses/

Create a stack that houses the opening brackets, if you see a closing bracket then the top of the stack SHOULD have that corresponding opening bracket.

```python
class Solution:
    def isValid(self, s: str) -> bool:
        mapping = { "}" : "{",
                    ")" : "(",
                    "]" : "["}

        stack = collections.deque()

        for i in s:

            # if closing bracket
            if i in mapping:
                # if the stacks most recent opening bracket matches this closing bracket
                if stack and stack[-1] == mapping[i]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(i) # not a closing bracket

        # stack only consists of opening brackets, so it should be empty
        return not stack
```
