# Lone Integer

{% hint style="info" %}
[https://binarysearch.com/problems/Lone-Integer](https://binarysearch.com/problems/Lone-Integer)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You are given a list of integers `nums` where each integer occurs exactly three times except for one which occurs once. Return the lone integer.

Bonus: can you do it in `O(1)` space?

**Constraints**

* `n ≤ 10,000` where `n` is length of `nums`

#### Example 1

**Input**

```text
nums = [2, 2, 2, 9, 5, 5, 5]
```
{% endtab %}

{% tab title="Answer" %}


Using math. You can sum the would be answer if all numbers were present. This is the sum of the set of nums \* 3, say this is ps.  
Then take the sum of nums, this is what you're given. say this is ss

divide the difference of the two sets by two which will give you the number with only one occurence.

\(ps - ss\) / 2 = number with only one occurence.

Explained differently

> Add each number once and multiply the sum by 3, we will get thrice the sum of each element of the array. Store it as thrice\_sum. Subtract the sum of the whole array from the thrice\_sum and divide the result by 2. The number we get is the required number \(which appears once in the array\).

This assumes all positive integers are given in the array.

```python
class Solution:
    def solve(self, nums):
        return (sum(set(nums)) * 3 - sum(nums)) / 2
```
{% endtab %}
{% endtabs %}

