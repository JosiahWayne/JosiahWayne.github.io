---
title: "[Leetcode] 11. Container With Most Water"
date: 2024-09-03
categories: 
  - "菜狗josiah的题解"
---

Following the daily question, today we are doing the problem 11 in Leetcode, a famous (?) problem: "Container With Most Water"

\[mathjax\]

> Firstly, let's take a look at the problem itself:
> 
> You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.  
> Find two lines that together with the x-axis form a container, such that the container contains the most water.  
> Return _the maximum amount of water a container can store_.  
> **Notice** that you may not slant the container.

<figure>

![](images/question_11.jpg)

<figcaption>

Picture form Leetcode

</figcaption>

</figure>

After gazing at the picture for (humm 3 mins), we can get a very easy way to calculate the water we can carry when we already know i and j, which is:

```
min(height[i], height[j]) * (j - i) 
# i is the left pointer and j is the right pointer.
```

$$ $$

So from this, we can get a brutal solution, which is to use two for loops to iterate all the possible solutions and get the largest water amount. This solution has a time complexity of $ O(n^2) $

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        ans = 0
        for i in range(len(height)):
            for j in range(i, len(height)):
                temp = 0
                if height[i] >= height[j]:
                    temp = height[j] * (j - i)
                    ans = max(ans, temp)
                elif height[i] < height[j]:
                    temp = height[i] * (j - i)
                    ans = max(ans, temp)
        return ans
```

How can we do better?

Looking deeper into this graph, we can notice a very interesting phenomenon.

For example, we let x as the left boundary and right as the right boundary, if $ x < y $ then no matter how we move the right boundary, the water amount will not increase, as $ W = min(x, y)\* t $(t is the gap length between left and right). We have two occasions:

First, $y\_{1} >= y$ then we still have $y\_{1} > x$, so $min(x, y\_{1}) = x$, $W = x \* t\_{1}$

Second, $y\_{1} <= y$, $ min(x, y\_{1}) < min(x, y) $

Thus, in order to get a bigger water amount, we have to try to change the smaller boundary, which might be able to help us reach the goal.

Thus is the reason why we can use the following way to solve the problem:

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        i = 0
        j = len(height) - 1
        w, ans = 0, 0
        while i < j:
            if height[i] >= height[j]:
                w = height[j] * (j - i)
                j -= 1
            else:
                w = height[i] * (j - i)
                i += 1
            ans = max(ans, w)
        return ans
```

Which can allow us to use double-pointer and only have to iterate the list once, providing us a $O(n)$ complexity.

This problem might be a little bit hard and took me a lot of time to go through the solution, I might try to rewrite the solution when I have more time or have a better knowledge.

_Citation:_ _This solution is inspired by the official solution from Leetcode:_ [link](https://leetcode.cn/problems/container-with-most-water/solutions/207215/sheng-zui-duo-shui-de-rong-qi-by-leetcode-solution)
