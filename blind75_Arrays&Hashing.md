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
-建立一个set，set只能存储一个元素一次，用.add()添加元素

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
-先比较长度
-用hashmap, 本质上是字典, key:value对, 比较两个hashmap是否完全相同
-Counter[key] -> value
-for loop字典, loop出的是key
-字典记得: 用.get(key, 0): -> 取key的value, 如果没出现过取0

OR

-比较sorted()后的字符是否一模一样

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

# 1. Two Sum
## 题目
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Input: nums = [3,2,4], target = 6
Output: [1,2]

## 思路
-for i,v in enumerate(nums) -> enumerate()的结果先是index, 再是value. 但是hashmap是value:index
-用hashmap储存value:index
-diff = target - v
-如果diff在hashmap里(ie 之前出现过), 就return v和diff的indices

## Code
```python
    class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        PrevMap = {} # val : index
        for i, v in enumerate(nums):
            diff = target - v
            if diff in PrevMap:
                return [PrevMap[diff], i]
            PrevMap[v] = i
```
## Complexity
time:O(n)
space:O(n)

# 49. Group Anagram
## 题目
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

input: strs = ["eat","tea","tan","ate","nat","bat"]

Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Explanation:

There is no string in strs that can be rearranged to form "bat".
The strings "nat" and "tan" are anagrams as they can be rearranged to form each other.
The strings "ate", "eat", and "tea" are anagrams as they can be rearranged to form each other.

## 思路
-defaultdict(list)创建key:list对, 当key不存在时自动创建空list绑定key
-用hashmap, key是list of count of all characters(from a to z), 但是python不能用list做key, 所以要改为tuple
-count作为每个词的list, index是ASCII码(距离"a"的), value是出现次数
-hashmap[key].append(value)用于已经有value时
-hashmap[key] = value用于还没有value时
-list(hashmap.values())把values以list形式return

## Code
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord("a")] += 1
            res[tuple(count)].append(s)
        return list(res.values())
```

## Complexity
Time: O(m*n)
Space: O(m*n)