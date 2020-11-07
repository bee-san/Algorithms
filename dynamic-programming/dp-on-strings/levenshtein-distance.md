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
{% embed url="https://leetcode.com/problems/edit-distance/discuss/159295/Python-solutions-and-intuition" %}

For those having difficulty cracking dynamic programming solutions, I find it easiest to solve by first starting with a naive, but working recursive implementation. It's essential to do so, because dynamic programming is basically recursion with caching. With this workflow, deciphering dynamic programming problems becomes just a little more manageable for us normal people. :\)

**Thought process:**  
Given two strings, we're tasked with finding the minimum number of transformations we need to make to arrive with equivalent strings. From the get-go, there doesn't seem to be any way around trying all possibilities, and in this, possibilities refers to inserting, deleting, or replacing a character. Recursion is usually a good choice for trying all possilbilities.

Whenever we write recursive functions, we'll need some way to terminate, or else we'll end up overflowing the stack via infinite recursion. With strings, the natural state to keep track of is the index. We'll need two indexes, one for word1 and one for word2. Now we just need to handle our base cases, and recursive cases.  
What happens when we're done with either word? Some thought will tell you that the minimum number of transformations is simply to insert the rest of the other word. This is our base case. What about when we're not done with either string? We'll either match the currently indexed characters in both strings, or mismatch. In the first case, we don't incur any penalty, and we can continue to compare the rest of the strings by recursing on the rest of both strings. In the case of a mismatch, we either insert, delete, or replace. To recap:
{% endtab %}
{% endtabs %}

