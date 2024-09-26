# Longest Repeating Character Replacement <img align="right" height="50" src="https://upload.wikimedia.org/wikipedia/commons/8/8e/LeetCode_Logo_1.png"/>

The key condition is this question is figuring out the calculation to deem a substring **valid**. If we take the length of the substring and subtract the most frequent character, we get how many characters we can replace. If this amount is LESS than $k$, we can calculate a max length.

There is an optimization for finding the most frequent character which is used below. It’s based on the fact we want the **largest** length so in order to **minimize $k$** in the same process, we need to also have the highest max frequency.

- when we increment the left pointer, we don’t need to decrement the maxf count
  - why? remember $length-maxf \leq k$
  - we want to maximize the length as that’s what we want to return
  - minimize the total $length-maxf$ to keep within the restriction of the constant $k$
  - therefore, reducing maxf won’t ever help us get a larger length so it doesn’t matter

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        freq = {}
        l = 0
        maxCount = 0
        maxf = 0

        for r in range(len(s)):
            freq[s[r]] = 1 + freq.get(s[r], 0)
            maxf = max(maxf, freq[s[r]])

            if (r - l + 1) - maxf <= k:
                maxCount = max(maxCount, r - l + 1)
            else:
                freq[s[l]] -= 1
                l += 1

        return maxCount
```
