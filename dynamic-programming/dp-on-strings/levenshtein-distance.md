# Levenshtein Distance

{% hint style="info" %}
[https://leetcode.com/problems/edit-distance/](https://leetcode.com/problems/edit-distance/)
{% endhint %}

This question is a leetcode hard, but in my opinion it is easier than the next problem which is a leetcode medium.

{% tabs %}
{% tab title="Question" %}
Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

```text
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```
{% endtab %}

{% tab title="Answer" %}
For those having difficulty cracking dynamic programming solutions, I find it easiest to solve by first starting with a naive, but working recursive implementation. It's essential to do so, because dynamic programming is basically recursion with caching. With this workflow, deciphering dynamic programming problems becomes just a little more manageable for us normal people. :\)
{% endtab %}
{% endtabs %}

