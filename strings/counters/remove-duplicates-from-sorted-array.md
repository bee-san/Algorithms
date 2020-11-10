# Remove Duplicates from Sorted Array

{% hint style="info" %}
[https://leetcode.com/problems/remove-duplicates-from-sorted-array/](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
{% endhint %}

If a question mentions a specific property about the input data, often the optimal solution will make use of this property.

In this case, we are told that the array is sorted. That means our optimal solution must make use of the fact it is sorted.

Listen carefully to what your interviewer is telling you, every word might come in handy.

{% tabs %}
{% tab title="Question" %}
Given a sorted array _nums_, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appears only _once_ and returns the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.
{% endtab %}

{% tab title="Answer" %}
```python
counter = 0
# We use while loop to try and cut down on 2 loops
while counter < (len(nums) - 1):
    # if current counter is the same as the next one
    # remove current
    if nums[counter] == nums[counter + 1]:
        nums.remove(nums[counter])
    else:
        # else they are not the same, so counter +=1
        counter += 1
return len(nums)
```
{% endtab %}
{% endtabs %}





