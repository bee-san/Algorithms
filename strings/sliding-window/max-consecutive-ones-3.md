# Max Consecutive Ones 3

{% hint style="info" %}
[https://leetcode.com/problems/max-consecutive-ones-iii/](https://leetcode.com/problems/max-consecutive-ones-iii/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `A` of 0s and 1s, we may change up to `K` values from 0 to 1.

Return the length of the longest \(contiguous\) subarray that contains only 1s. 

**Example 1:**

```text
Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation: 
[1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
```
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def longestOnes(self, A: List[int], K: int) -> int:
        self.answer = 0
        start, end, zeros, length = 0, 0, 0, 0

        while end < len(A):
            if A[end] == 0:
                zeros += 1

            while zeros > K:
                if A[start] == 0:
                    zeros -= 1
                length -= 1
                start += 1

            length += 1
            self.answer = length if length > self.answer else self.answer
            end += 1

        return self.answer
```
{% endtab %}
{% endtabs %}

