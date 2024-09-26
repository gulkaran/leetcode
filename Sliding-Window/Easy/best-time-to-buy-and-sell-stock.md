# Best Time To Buy and Sell Stock <img align="right" height="50" src="https://upload.wikimedia.org/wikipedia/commons/8/8e/LeetCode_Logo_1.png"/>

If our selling pointer is less than our buy one, update the buy, so it's the lowest sell price we've seen to maximize profit.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buy, sell = 0, 0

        maxProfit = 0

        while sell < len(prices):

            if prices[sell] < prices[buy]:
                buy, sell = sell, sell + 1
            else:
                maxProfit = max(maxProfit, prices[sell] - prices[buy])
                sell += 1

        return maxProfit
```
