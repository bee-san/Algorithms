# Climbing Stairs

{% hint style="info" %}
[https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You are climbing a stair case. It takes _n_ steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

```text
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
{% endtab %}

{% tab title="Answer" %}
```python
# The answer is the same as the example
# It's also Fibonacci
# This post explains it well
# https://leetcode.com/problems/climbing-stairs/discuss/25299/Basically-it's-a-fibonacci.
class Solution:
    def climbStairs(self, n: int) -> int:
        if not n:
            return None
        if n == 1:
            return 1
        if n == 2:
            return 2
        
        d = [float("inf") for i in range(n)]
        d[0] = 1
        d[1] = 2
        for i in range(2, n):
            d[i] = d[i - 1] + d[i - 2]
        return d[-1]
        
```
{% endtab %}
{% endtabs %}



