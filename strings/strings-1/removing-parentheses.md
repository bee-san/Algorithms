# Removing Parentheses

{% hint style="info" %}
[https://binarysearch.com/problems/Removing-Parentheses](https://binarysearch.com/problems/Removing-Parentheses)

I know it's not Leetcode please don't kill me. I was in a competition and I thought this was neat. Couldn't find the leetcode alternative.
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a string of parentheses `s`, return the minimum number of parentheses to be removed to make the string valid \(i.e. each open parenthesis is eventually closed\).

For example, given the string `"()())()"`, you should return 1. Given the string `")("`, you should return 2, since we must remove all of them.
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def solve(self, s):
        """
        first thought is we track ( and )
        if we one is higher than the other, we remove it
        """
        if not s:
            return 0
        total = 0
        temp = 0
        for p in s:
            if p == "(":
                total += 1
            elif p == ")" and total:
                # the and total means this only runs if total is more than 0
                # so we only have ) if we have ( before it
                total -= 1
            else:
                temp += 1
        return total + temp
```

We keep track of 2 variables:

* Total \(will be 0 if we have the same number of \( and \).
* Temp - will increment if we \) but no \( before it.
{% endtab %}
{% endtabs %}

