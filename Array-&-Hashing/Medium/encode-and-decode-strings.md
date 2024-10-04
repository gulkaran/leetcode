# Encode and Decode Strings

### Problem Description

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Please implement `encode` and `decode`. Note our input can have any any of the **256** legal ASCII characters, your algorithm must be able to handle any character that may appear.

**Example1**

```python
Input: ["lint","code","love","you"]
Output: ["lint","code","love","you"]
Explanation:
One possible encode method: "lint:;code:;love:;you"
```

**Common Issues**

```python
[ "hello", "wo#rld" ] -> encode -> "hello#wo#rld" -> decode -> ["hello", "wo", "rld"]
```

Can’t just join and split based on an ascii character. 

### Solution

Join based on the **length** of the word with a delimiter symbol. The reason for this is because our inputs can have random numbers in there but the delimiter lets us uniquely identify that this is the start of the next word.

We put the length and delimiter directly into the string.

```python
[ "hello", "wo#rld" ] -> "5#hello6#wo#rld"
```

This 5# tells us the word is 5 characters in length and lets us decode it.

```python
# preprends the length + delimiter
def encode(strs):
        res = ""
        for i in strs:
            res += str(len(i)) + "#" + i
        return res

# finds num before delimter, and string splicing to append words
def decode(str):
    res = []
    i = 0

    while i < len(str):
        # we do this to find the number before the #
        # could be large like 100#...
        j = i
        while str[j] != "#":
             j += 1
        
        count = int(str[i:j])
        res.append(str[j+1:j+1+count])
        i = j + 1 + count
    return res

strs = ["hello", "wo$!!@#!@ASasd241241rld"]

print(encode(strs))
print(decode(encode(strs)))
```