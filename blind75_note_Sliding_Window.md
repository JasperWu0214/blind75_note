# 3. Longest Substring Without Repeating Characters
## 题目
Given a string s, find the length of the longest substring without duplicate characters.

Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3. Note that "bca" and "cab" are also correct answers.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

## 思路
- 用set检查duplicate: 添加：set.add(); 删除:set.remove()
- L和R构成sliding window, L固定, 用R遍历
- 遇到重复情况: 把L的元素从set中删除, 再increment L [while loop]
- 每次for loop要max(), ie在窗口清理完后

## Code
```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l = 0
        res = 0
        charset = set()
        for r in range(len(s)):
            while s[r] in charset:
                charset.remove(s[l])
                l += 1
            charset.add(s[r])
            res = max(res, r-l+1)
        return res
```

## Complexity
Time: O(n)
Spcae: O(n)