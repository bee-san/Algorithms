# List Partitoning

{% hint style="info" %}
[https://binarysearch.com/problems/List-Partitioning](https://binarysearch.com/problems/List-Partitioning)

^^ Not leetcode, but the problem was nice.
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a list of strings `strs`, containing the strings `"red"`, `"green"` and `"blue"`, partition the list so that the red come before green, which come before blue.

**Constraints**

* `n ≤ 100,000` where `n` is the length of `strs`.

This should be done in \mathcal{O}\(n\)O\(n\) time.

Bonus: Can you do it in \mathcal{O}\(1\)O\(1\) space? That is, can you do it by only rearranging the list \(i.e. without creating any new strings\)?

#### Example 1

**Input**

```text
strs = ["green", "blue", "red", "red"]
```

**Output**

```text
["red", "red", "green", "blue"]
```
{% endtab %}

{% tab title="Answer" %}
Start from the beginning swapping in all reds. Picking up where that left off, swap in all greens. All blues are where they need to be.

```python
class Solution:
    def solve(self, s):
        def partition(s, start, word):
            for i in range(start, len(s)):
                if s[i] == word:
                    s[i], s[start] = s[start], s[i]
                    start += 1
            return start

        start = partition(s, 0, "red")
        partition(s, start, "green")
        return s
```
{% endtab %}
{% endtabs %}

