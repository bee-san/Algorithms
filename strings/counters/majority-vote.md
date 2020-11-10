# Majority Vote

{% hint style="info" %}
[https://leetcode.com/problems/majority-element/](https://leetcode.com/problems/majority-element/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array of size n, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```text
Input: [3,2,3]
Output: 3
```
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        cnt = 0
        maj = 0
        for i in nums:
            if cnt == 0:
                maj = i
            cnt += 1 if maj == i else -1
        return maj
```

We increment the counter if we come across `maj` as the majority. Else we decrement it. 

If we have 4 elements. 3 are "1" and 1 is "2". We will end up with 3 as the majority.

Note we need to perform another pass to count if it's truly the majority and has won by n/2 votes. This is guaranteed in this problem.
{% endtab %}
{% endtabs %}

