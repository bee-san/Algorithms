# Split array largest sum

{% hint style="info" %}
[https://leetcode.com/problems/split-array-largest-sum/](https://leetcode.com/problems/split-array-largest-sum/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `nums` which consists of non-negative integers and an integer `m`, you can split the array into `m` non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these `m` subarrays.

```text
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```
{% endtab %}

{% tab title="Answer" %}
If you take a close look, you would probably see how similar this problem is with LC 1011 above. Similarly, we can design a `feasible` function: given an input `threshold`, then decide if we can split the array into several subarrays such that every subarray-sum is less than or equal to `threshold`. In this way, we discover the monotonicity of the problem: if `feasible(m)` is `True`, then all inputs larger than `m` can satisfy `feasible` function. You can see that the solution code is exactly the same as LC 1011.

```python
def splitArray(nums: List[int], m: int) -> int:        
    def feasible(threshold) -> bool:
        count = 1
        total = 0
        for num in nums:
            total += num
            if total > threshold:
                total = num
                count += 1
                if count > m:
                    return False
        return True

    left, right = max(nums), sum(nums)
    while left < right:
        mid = left + (right - left) // 2
        if feasible(mid):
            right = mid     
        else:
            left = mid + 1
    return left
```

But we probably would have doubts: It's true that `left` returned by our solution is the minimal value satisfying `feasible`, but how can we know that we can split the original array to **actually get this subarray-sum**? For example, let's say `nums = [7,2,5,10,8]` and `m = 2`. We have 4 different ways to split the array to get 4 different largest subarray-sum correspondingly: `25:[[7], [2,5,10,8]]`, `23:[[7,2], [5,10,8]]`, `18:[[7,2,5], [10,8]]`, `24:[[7,2,5,10], [8]]`. Only 4 values. But our search space `[max(nums), sum(nums)] = [10, 32]` has much more that just 4 values. That is, no matter how we split the input array, we cannot get most of the values in our search space.

Let's say `k` is the minimal value satisfying `feasible` function. We can prove the correctness of our solution with proof by contradiction. Assume that no subarray's sum is equal to `k`, that is, every subarray sum is less than `k`. The variable `total` inside `feasible` function keeps track of the total weights of current load. If our assumption is correct, then `total` would always be less than `k`. As a result, `feasible(k - 1)` must be `True`, because `total` would at most be equal to `k - 1` and would never trigger the if-clause `if total > threshold`, therefore `feasible(k - 1)` must have the same output as `feasible(k)`, which is `True`. But we already know that `k` is the minimal value satisfying `feasible` function, so `feasible(k - 1)` has to be `False`, which is a contradiction. So our assumption is incorrect. Now we've proved that our algorithm is correct.
{% endtab %}
{% endtabs %}

