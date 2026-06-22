Arrays & Hashing

# 217. Contains Duplicate

## 题目
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Input: nums = [1,2,3,1]
Output: true
Explanation:
The element 1 occurs at the indices 0 and 3.

Input: nums = [1,2,3,4]
Output: false
Explanation:
All elements are distinct.

## Code
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        hashset = set()
        for i in nums:
            if i in hashset:
                return True
            hashset.add(i)
        return False
```
## 思路
建立一个set，set只能存储一个元素一次，用.add()添加元素

## 复杂度
Time Complexity: O(n)
Space Complexity: O(n)


# 242. Valid Anagram 变位词
## 题目
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

Input: s = "anagram", t = "nagaram"
Output: true

Input: s = "rat", t = "car"
Output: false

## 思路
先比较长度
用hashmap, 本质上是字典, key:value对, 比较两个hashmap是否完全相同
Counter[key] -> value
for loop字典, loop出的是key
用.get(key, 0): 取key的value, 如果没出现过取0
OR
比较sorted()后的字符是否一模一样

## Solution 1
### Code 1
``` python
    class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        CounterS, CounterT = {}, {}
        if len(s) != len(t):
            return False
        for c in range(len(s)):
            CounterS[s[c]] = 1 + CounterS.get(s[c], 0)
            CounterT[t[c]] = 1 + CounterT.get(t[c], 0)
        for n in CounterS:
            if CounterS[n] != CounterT.get(n, 0):
                return False
        return True
```
``` python
    class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```
### Complexity 1
time: O(s+t)
space: O(s+t)

## Solution 2
### Code 2
```python
    class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```
### Complexity 2
time: O(nlogn) OR O(n^2)
space: O(1) OR O(n) depends on the sorting algorithm
