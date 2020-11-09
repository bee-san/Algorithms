# Check If N and Its Double Exist

{% hint style="info" %}
[https://leetcode.com/problems/check-if-n-and-its-double-exist/](https://leetcode.com/problems/check-if-n-and-its-double-exist/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `arr` of integers, check if there exists two integers `N` and `M` such that `N` is the double of `M` \( i.e. `N = 2 * M`\).

More formally check if there exists two indices `i` and `j` such that :

* `i != j`
* `0 <= i, j < arr.length`
* `arr[i] == 2 * arr[j]`

**Example 1:**

```text
Input: arr = [10,2,5,3]
Output: true
Explanation: N = 10 is the double of M = 5,that is, 10 = 2 * 5.
```
{% endtab %}

{% tab title="Answer" %}
count all numbers and store in counter,

1. if there are multiple zero return True
2. check each number's double in counter, if it is at least one, return True,
3. return False if above conditions fail

```python
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        count = collections.Counter(arr)
        for i in arr:
            if count[i*2] and i != 0 or count[0] > 1 :
                return True
        return False
```
{% endtab %}
{% endtabs %}

