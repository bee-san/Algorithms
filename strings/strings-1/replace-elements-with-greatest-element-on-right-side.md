# Replace Elements with Greatest Element on Right Side

{% hint style="info" %}
[https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `arr`, replace every element in that array with the greatest element among the elements to its right, and replace the last element with `-1`.

After doing so, return the array.

**Example 1:**

```text
Input: arr = [17,18,5,4,6,1]
Output: [18,6,6,6,1,-1]
```
{% endtab %}

{% tab title="Answer" %}
From [here](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/discuss/463249/JavaC%2B%2BPython-Straight-Forward).

 Iterate from the back to the start,  
We initilize `mx = 1`, where `mx` represent the max on the right.  
Each round, we set `A[i] = mx`, where `mx` is its mas on the right.  
Also we update `mx = max(mx, A[i])`, where `A[i]` is its original value.

```python
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        A = arr
        mx = -1
        for i in range(len(A) - 1, -1, -1):
            A[i], mx = mx, max(mx, A[i])
        return A
```
{% endtab %}
{% endtabs %}

