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

# 15. 3Sum
## 题目
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
Notice that the solution set must not contain duplicate triplets.

Example 1:
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

## 思路
- 先sort array, 利用2SumII的two pointers思路
- nested loop: 确定一个数, 再把后面initialise L, R pointers
- must distinct: 遇到相同元素跳过(并且i>0，ie为array的第二个元素)
- edge case: 找到一组后, 后面还有其他满足条件的list, 要update L pointer
- 做法： 找到一组答案后先increment L, 再increment(当目前元素与前一个元素相同 and l<r 时)
- .append()只能用一个argument, [a, nums[l], nums[r]]

## Code
```py
class Solution:
    def threeSum(self, nums: list[int]) -> list[list[int]]:
        res = []
        nums.sort()

        for i, a in enumerate(nums):
            if i > 0 and a == nums[i-1]:
                continue

            l, r = i + 1, len(nums)-1
            while l < r:
                threeSum = a + nums[l] + nums[r]
                if threeSum > 0:
                    r -= 1
                elif threeSum < 0:
                    l += 1
                else:
                    res.append([a, nums[l], nums[r]])
                    l += 1
                    while nums[l] == nums[l-1] and l < r :
                        l += 1
                        
        return res
```

## Complexity
time: O(nlogn) + O(n^2) = O(n^2)
space: O(1)