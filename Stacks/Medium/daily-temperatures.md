# Daily Temperatures

[https://leetcode.com/problems/daily-temperatures/](https://leetcode.com/problems/daily-temperatures/)

This stack problem follows the concept that the elements in the stack are decreasing. We store the indices of the temperatures in the stack, and whenever we come to a new temperature that is **greater** than the top of the stack, we calculate the difference in indices and store that in our answer array.

- $stack = [75,71,69]$
- $curr\_val =72$
- compare 72 > 69, calculate index difference and store in answer array, pop 69
- compare 72 > 71, same process, pop 71
- compare 72 > 75 → false, so we push 72 to the stack
- $stack=[75,72]$

**Note**: a more clear solution would be to store $(temperature, index)$ in the stack as a tuple or node, however, you can get a more efficient solution by just storing the index. 

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0 for i in range(len(temperatures))]
        
        # decreasing stack
        stack = []

        for i in range(len(temperatures)):
            while stack and temperatures[i] > temperatures[stack[-1]]:
                answer[stack[-1]] = i-stack[-1]
                stack.pop()
            stack.append(i)
        
        return answer
```