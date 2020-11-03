# Consecutive Characters

{% hint style="info" %}
[https://leetcode.com/problems/consecutive-characters/](https://leetcode.com/problems/consecutive-characters/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a string `s`, the power of the string is the maximum length of a non-empty substring that contains only one unique character.

Return _the power_ of the string.

```text
Input: s = "leetcode"
Output: 2
Explanation: The substring "ee" is of length 2 with the character 'e' only.
```
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def maxPower(self, s: str) -> int:
        powers = [None for x in range(len(s))]
        powers[0] = 1
        for i in range(1, len(powers)):
            if s[i] == s[i - 1]:
                powers[i] = powers[i - 1] + 1
            else:
                powers[i] = 1
        return max(powers)
```

We generate a list of all possible powers.

The base case is:

* \[0\] = 1, since there are no letters before.

And then for each power, it is either:  


* The previous power + 1 \(because its a continuation of the substring + 1 char since the chars are the same\)

```text
aaab
[4, 5]
i[2] = i[2 - 1] + 1 because "a" at index 2 == "a" at index 1.
```

* 1, because it's a new substring

We then return the maximum possible value over our array.
{% endtab %}
{% endtabs %}

