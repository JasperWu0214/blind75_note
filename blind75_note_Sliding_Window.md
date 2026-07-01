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

# 121. Best time to buy and sell stock
## 题目
You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

## 思路
- Buy low, Sell high.
- l固定, 如果遇到更低的就把l移过去(buy low). 
- r loop through, 每个iteration max(maxP, currentP) (sell high)

## Code
```py
    class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l, r = 0, 1
        maxP = 0
        while r < len(prices):
            currentP = prices[r] - prices[l]
            maxP = max(maxP, currentP)
            while prices[l] > prices[r]:
                l = r
            r += 1
        return maxP
```