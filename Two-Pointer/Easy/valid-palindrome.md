# Valid Palindrome

[https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

Honestly, not much of a trick. Use **two pointers** (start and end) and compare if they are alphanumeric. Use ascii to accomplish this.

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:

        i, j = 0, len(s) - 1

        while i < j:

            while not self.isAlphanumeric(s[i]) and i < j:
                i += 1

            while not self.isAlphanumeric(s[j]) and j > i:
                j -= 1

            if s[i].lower() != s[j].lower():
                return False
            
            i, j = i + 1, j - 1

        return True

    def isAlphanumeric(self, c: int):
        
        return (ord('A') <= ord(c) <= ord('Z') or 
                ord('a') <= ord(c) <= ord('z') or
                ord('0') <= ord(c) <= ord('9'))

```