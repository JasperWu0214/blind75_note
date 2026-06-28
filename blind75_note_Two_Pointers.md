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

# 167. Two Sum II - Input Array is sorted
## 题目
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.
Return the indices of the two numbers index1 and index2, each incremented by one, as an integer array [index1, index2] of length 2.
The tests are generated such that there is exactly one solution. You may not use the same element twice.
Your solution must use only constant extra space.

Example 1:
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

## 思路1
- 从index 1(index 0 in other case)开始, 比较后面的每一个数，看是否能满足target
- 但一旦两个数之和大于target, 就quit
- 不管i是否是最后一个, n都要赋值, 否则进入不了下一步, while n < len(numbers)保证边界
- quit部分numbers[i]+numbers[n] <= target， 不能是只有<，否则相等的情况就被排除了

## Code 1
```py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        for i in range(len(numbers)):
            n = i+1
            while n < len(numbers) and numbers[i]+numbers[n] <= target:
                if numbers[i] + numbers[n] == target:
                    return [i+1, n+1]
                n += 1
```

## Complexity 1
Time: O(n^2)
Space: O(1)

## 思路2
- two pointers: 两数之和小于则increment L, 大于则increment R

## Code 2
```py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers)-1
        while l<r:
            if numbers[l] + numbers[r] == target:
                return [l+1, r+1]
            elif numbers[l] + numbers[r] < target:
                l += 1
            else:
                r -= 1
```

## Complexity 2
Time: O(n)
Space: O(1)