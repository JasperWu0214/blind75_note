Two Pointers
# 125.Valid Palindrom
## 题目
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.
Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

## 思路 1
- alphanumeric: .isalnum() | convert into lowercase: .lower()
- 把符号去掉，字母全小写，如果reverse过后string还是一样就是palindrome
- string append用+=

## Code 1
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        newstr = ""
        for c in s:
            if c.isalnum():
                newstr += c.lower()
        return newstr == newstr[::-1]
```

## Complexity 1
Time: O(n)
Space: O(n)

## 思路2
- 自己写alphanum()函数, 用ASCII码, 判断是否在小写字母, 大写字母以及数字的ASCII码范围之间, 用ord()
- two pointers做法, 要initialise, keep in bound, skip, update四个环节
- 还要看题目，要lower()
- python中在class里调用另一个函数要self.alphanum()

## Code 2
```py
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s)-1 #initialisation
        while l < r: #keep in bound
            while l < r and self.alphanum(s[l]) == False: #skip
                l += 1
            while l < r and self.alphanum(s[r]) == False:
                r -= 1
            if s[l].lower() != s[r].lower():# determine, remember in lower case
                return False
            l, r = l+1, r-1 # update pointer
        return True
    def alphanum(self, c):
        if (ord("a") <= ord(c) <= ord("z") or
            ord("A") <= ord(c) <= ord("Z") or
            ord("0") <= ord(c) <= ord("9")):
            return True
        return False  
```

## Complexity 2
Time: O(n)
Space: O(1)