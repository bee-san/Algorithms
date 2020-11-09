# Move Zeros

{% hint style="info" %}
[https://leetcode.com/problems/move-zeroes/](https://leetcode.com/problems/move-zeroes/)
{% endhint %}

{% tabs %}
{% tab title="Answer" %}
Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```text
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.
{% endtab %}

{% tab title="Question" %}
```python
class Solution:
    def moveZeroes(self, nums):
        zero = 0  # records the position of "0"
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[i], nums[zero] = nums[zero], nums[i]
                zero += 1
```

We swap bubble the 0's up the array in-place.
{% endtab %}
{% endtabs %}

