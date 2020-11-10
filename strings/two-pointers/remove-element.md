# Remove Element

{% hint style="info" %}
[https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array _nums_ and a value _val_, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means a modification to the input array will be known to the caller as well.

Internally you can think of this:

```text
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
{% endtab %}

{% tab title="Answer" %}
Your first thought might be:

```python
class Solution(object):
    def removeElement(self, nums, val):
        for i in range(nums.count(val)):
            nums.remove(val)
        return len(nums)
```

This is bad because `.remove(val)` is O\(n\), making the solution O\(n^2\).

The optimal O\(n\) solution is:

```python
  def removeElement(self, nums, val):
    start, end = 0, len(nums) - 1
    while start <= end:
        if nums[start] == val:
            nums[start], nums[end], end = nums[end], nums[start], end - 1
        else:
            start +=1
    return start
```

From here [https://leetcode.com/problems/remove-element/discuss/12306/Simple-Python-O\(n\)-two-pointer-in-place-solution](https://leetcode.com/problems/remove-element/discuss/12306/Simple-Python-O%28n%29-two-pointer-in-place-solution) :

> Starting from the left every time we find a value that is the target value we swap it out with an item starting from the right. We decrement end each time as we know that the final item is the target value and only increment start once we know the value is ok. Once start reaches end we know all items after that point are the target value so we can stop there.
{% endtab %}
{% endtabs %}



