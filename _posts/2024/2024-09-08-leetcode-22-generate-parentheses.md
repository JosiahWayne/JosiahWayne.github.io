---
title: "[Leetcode] 22. Generate Parentheses"
date: 2024-09-08
categories: 
  - "菜狗josiah的题解"
---

\[mathjax\]

This is quite an interesting question... I used DP to solve this problem(Absolutely not because I checked the answer lol.) I think this question can be used as a great example on how to use DP and in which case DP can be used to program.

First, let's take a look at the question description:

> Given `n` pairs of parentheses, write a function to _generate all combinations of well-formed parentheses_.

Humm when I first got the question, it took me really long time to think how should I solve the problem (cuz im too stupid...)

At first I think it might be a really great way to solve the problem in a DP way, thats because parentheses is a kind of thing that will lead you to consider consider the nested relation ship between different layers. However, probably because it is months ago since the last time I solve a DP problem. I failed to came out how the hail should I program.

After having a glance at a solution, the question suddenly became really clear to me.

First, let us think about the first parenthesis. The left-most digit must be a "(", as it will be illegal if it is a ")". Thus we generate our first pair of parenthesis. In general situations with $ n $ pairs of parentheses, we still have $n-1$ pairs to consider. In this case, there are only two places that the remaining parentheses can be placed into. Inside of the generated parentheses, or right side of the generated parentheses. And as there are $n-1$ pairs in total. We will put $p$ pairs inside and $n - 1 - p$ pairs right side. And in this case, we only need to get `generateParenthesis(p)` and `generateParenthesis(n - 1 - p)` And then calculate all the assembly.

```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        if n == 0:
            return ['']
        if n == 1:
            return['()']
 
        re = []
        for i in range(n):
            left = self.generateParenthesis(i) # calculate the possibilities which should be inside.
            right = self.generateParenthesis(n - 1 - i) # calculate the possibilities which should be on right side.
            for j in left:
                for k in right:
                    re.append(f"({j}){k}")
        return re
```

This solution is inspired by [link](https://leetcode.cn/problems/generate-parentheses/solutions/9251/zui-jian-dan-yi-dong-de-dong-tai-gui-hua-bu-lun-da).
