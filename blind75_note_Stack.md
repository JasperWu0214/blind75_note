Stack
# 20. Valid Parentheses
## 题目
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:
Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.

Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "()[]{}"
Output: true

Example 5:
Input: s = "([)]"
Output: false

## 思路
- hashmap存close bracket : open bracket
- 用stack存储open bracket
- hashmap遇到的值: close bracket, stack遇到的值: open bracket
- if c in 字典, 只会匹配字典的key, 字典的value不会匹配
- stack[-1]含义: 最后一个append进list的值
- 还需要检测stack是否为空: 应对edge case, ie 比较第一个值, stack为True如果有值

## Code
```py
    class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        parentheses = {')':'(', ']':'[', '}':'{'}
        for c in s:
            if c in parentheses:
                if stack and stack[-1] == parentheses[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return True if not stack else False
```

# Complexity
Time:O(n)
Space:O(n)

