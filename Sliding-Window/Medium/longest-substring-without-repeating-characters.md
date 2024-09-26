# Longest Substring Without Repeating Characters <img align="right" height="50" src="https://upload.wikimedia.org/wikipedia/commons/8/8e/LeetCode_Logo_1.png"/>

Create a sliding window where if the **right** most pointer see’s a character we’ve already seen, increment the left until its not in the set. After that, we can add it to the set and calculate the max height.

- ‘abc**a**bc’ → right pointer goes to second a (r = 3), while that a is in the set, remove it from the left most side (and increment left pointer). When it’s not in the set anymore (out of the while loop), we know our substring is valid again, so we can continue searching.

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set()
        l = 0
        maxCount = 0

        for r in range(len(s)):
            while s[r] in seen:
                seen.discard(s[l])
                l += 1
            seen.add(s[r])
            maxCount = max(maxCount, r - l + 1)

        return maxCount
```
