# Search Insert Position

{% hint style="info" %}
[https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

```text
Input: nums = [1,3,5,6], target = 5
Output: 2
```
{% endtab %}

{% tab title="Answer" %}
* When do we exit the loop? 

We exit the loop if left &lt; right

* How to initialise the boundary variable left and right

Left is set to 0. If our target value is larger than every val in the array, we want it to be placed at the end. So right is up to len\(right\), instead of len\(right\) - 1

* How to update the boundary? How to choose the appropriate combination from `left = mid, left = mid + 1` and `right = mid, right = mid - 1`?

We just want the normal search here. Right = mid, left = mid + 1.

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)
        while l < r:
            mid = (l + r) // 2
            if nums[mid] >= target:
                r = mid
            else:
                l = mid + 1
        return l
```

Perfectly normal binary search! We go from the left to the right because it is sorted. When we hit `len(nums)` we are at a position that doesn't exist yet, so we return that position to be the point where `target` is supposed to be inserted.

This is because target is greater than the maximum value of the array.
{% endtab %}
{% endtabs %}

