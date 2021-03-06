# Longest Common Subsequence

{% hint style="info" %}
[https://leetcode.com/problems/longest-common-subsequence/](https://leetcode.com/problems/longest-common-subsequence/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given two strings `text1` and `text2`, return the length of their longest common subsequence.

A _subsequence_ of a string is a new string generated from the original string with some characters\(can be none\) deleted without changing the relative order of the remaining characters. \(eg, "ace" is a subsequence of "abcde" while "aec" is not\). A _common subsequence_ of two strings is a subsequence that is common to both strings.

If there is no common subsequence, return 0.
{% endtab %}

{% tab title="Answer" %}
{% embed url="https://www.youtube.com/watch?v=ASoaQq66foQ" %}

Let's look at the base case here.

Per the question:

> A subsequence of a string is a new string generated from the original string with some characters **`(can be none)`** deleted without changing the relative order of the remaining characters.

It can be none.

That means for any 2 strings:

* The minimum substring is 1.

We should keep track of the longest common substring for every possible combination.

![](../../.gitbook/assets/image%20%2812%29.png)

Because we have empty strings, the values for each empty string is 0.  
If we are filling in \(a, a\) we ask ourselves if we have string "a" and "a" and nothing else, what will be the longest subsequence?  
The length of the common subsequence is 1 here. Note: When we read the top, we are reading it as `["a", "ab", "abc"]`.

![](../../.gitbook/assets/image%20%2815%29.png)

With only the letter "a" we can only make at most 1 subsequence with all of them.  
Our third row now includes c as well as a for "ac".

![](../../.gitbook/assets/image%20%2814%29.png)

We compare "abc" with "ac". Since 2 letters are the same our value is 2.

![](../../.gitbook/assets/image%20%2811%29.png)

We choose the maximum of these 2 values. 2 is the maximum so we use it here.

Our value here is 3 + 1 which is 4.

![](../../.gitbook/assets/image%20%288%29.png)

And we are done!
{% endtab %}
{% endtabs %}

