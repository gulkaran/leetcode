# Evaluate Reverse Polish Notation

[https://leetcode.com/problems/evaluate-reverse-polish-notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/description/)/

Every time you see a operator, you pop twice from the operands stack, compute the operation, and push the result back onto the stack.

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:

        operands = []
        ops = { "+", "-", "/", "*" }

        for token in tokens:
            if token in ops:
                second_operand = operands.pop()
                first_operand = operands.pop()

                if token == "+":
                    result = (first_operand + second_operand)
                elif token == "-":
                    result = (first_operand - second_operand)
                elif token == "/":
                    result = int(first_operand / second_operand)
                else:
                    result = (first_operand * second_operand)

                operands.append(result)

            else:
                operands.append(int(token))

        return operands.pop()
```

Fun fact, this was an example done in COMPSCI 2C03!