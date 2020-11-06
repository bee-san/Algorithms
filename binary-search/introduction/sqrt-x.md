# Sqrt\(x\)

{% hint style="info" %}
[https://leetcode.com/problems/sqrtx/](https://leetcode.com/problems/sqrtx/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Implement `int sqrt(int x)`.

Compute and return the square root of _x_, where _x_ is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

```text
Input: 4
Output: 2
```
{% endtab %}

{% tab title="Answer" %}
We usually look for the minimal value that satisfies the condition, but in this problem we are looking for the maximal value instead.

The maximal value satisfying `condition(k) is False` is equal to `condition(k) is True` minus 1. 

This is shy we need to decide which value to return, left or left -1.

Let's look at this in more detail.

Our condition is:

```python
def condition(mid):
    return mid * mid <= x
```

Given the number 4, we have this array:

```python
[0, 1, 2, 3]
```

This means our array looks like:

```text
0 * 0 <= x: True
1 * 1 <= x: True
2 * 2 <= x: True
3 * 3 <= x: False

[True, True, True, False]
```

So our search needs to find the maximal value that does not equate to False. To do that. Let's look at what happens to our left and right pointers as we move along.

Our pointers are:

* left = 0
* right = 4

We now begin looping.

* Mid = 2

0 \* 0 &lt;= x, so we change our left pointer to mid + 1, which is 2 + 1.

* Left = 3
* right = 4
* Mid = 3 + \(4 - 3\) // 2 = 3

Now we calculate for mid again. 3\*3 is not &lt;= 4, so we change our right pointer to mid.

* left = 3
* right = 3
* mid = 3

We exit out loop because 3 is not valid. Because 3 is not valid, we return the element right before 3 which is 2. 

Therefore our answer is 2.

If you recall our normal binary search:

```python
    left, right = 0, len(array)
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            right = mid
        else:
            left = mid + 1
    return left
```

We've switched around right and mid. Let's see what'd happen if we went with this.

This is because we usually look for the minimal value that satisfies the condition \(thus we want to use the right to calculate this\), but in this case we are looking for the maximal value instead \(so we want to use left\).  
  
This is because **the array is sorted**. Moving right implies that we are looking for the minimal value, as the smallest values come first.

Because the array is sorted in increasing order, the largest value is always last. So we use left to find that value

And now our code looks like:

```python
def mySqrt(x: int) -> int:
    def condition(mid):
        return mid * mid <= x
    
    left, right = 0, x
    while left < right:
        mid = left + (right - left) // 2
        if condition(mid):
            left = mid + 1
        else:
            right = mid
    return left - 1
```
{% endtab %}
{% endtabs %}



