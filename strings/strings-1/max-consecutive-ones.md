# Max Consecutive Ones

{% hint style="info" %}
[https://leetcode.com/problems/max-consecutive-ones/](https://leetcode.com/problems/max-consecutive-ones/)
{% endhint %}



{% tabs %}
{% tab title="Question" %}
In this question we are asked:

> Given a binary array, find the maximum number of consecutive 1s in this array.

```text
Input: [1,1,0,1,1,1]
Output: 3
```
{% endtab %}

{% tab title="Answer" %}
This is a for loop through the array, keeping 2 counters.

For every num in the array, we check to see if it is a 1. If it is, we += 1 to the counter. If it's not, we reset the counter.

Everytime we see a 1, we set the answer to the maximum\(current\_answer, count\). 

We then return the answer.

```python
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        count = 0
        ans = 0
        for num in nums:
            if num == 1:
                count += 1
                ans = max(ans, count )
            else:
                cnt = 0
        return ans
```

This algorithm is O\(n\) time. As it touches every item in the array exactly once, and the array can be of size N.

The space complexity is O\(n\) space.
{% endtab %}
{% endtabs %}

Click "Answer" tab to see the answer. Try to do it yourself first!

