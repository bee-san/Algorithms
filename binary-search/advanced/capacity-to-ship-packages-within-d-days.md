# Capacity to Ship Packages within D Days



{% hint style="info" %}
[https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
A conveyor belt has packages that must be shipped from one port to another within `D` days.

The `i`-th package on the conveyor belt has a weight of `weights[i]`.  Each day, we load the ship with packages on the conveyor belt \(in the order given by `weights`\). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `D` days.

```text
Input: weights = [1,2,3,4,5,6,7,8,9,10], D = 5
Output: 15
Explanation: 
A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed. 
```
{% endtab %}

{% tab title="Answer" %}
Binary search probably would not come to our mind when we first meet this problem. We might automatically treat `weights` as search space and then realize we've entered a dead end after wasting lots of time. In fact, we are looking for the minimal one among all feasible capacities. 

We dig out the monotonicity of this problem: if we can successfully ship all packages within `D` days with capacity `m`, then we can definitely ship them all with any capacity larger than `m`. 

Now we can design a `condition` function, let's call it `feasible`, given an input `capacity`, it returns whether it's possible to ship all packages within `D` days. 

This can run in a greedy way: if there's still room for the current package, we put this package onto the conveyor belt, otherwise we wait for the next day to place this package. If the total days needed exceeds `D`, we return `False`, otherwise we return `True`.

Next, we need to initialize our boundary correctly. Obviously `capacity` should be at least `max(weights)`, otherwise the conveyor belt couldn't ship the heaviest package. On the other hand, `capacity` need not be more than`sum(weights)`, because then we can ship all packages in just one day.

Now we've got all we need to apply our binary search template:

```python
def shipWithinDays(weights: List[int], D: int) -> int:
    def feasible(capacity) -> bool:
        days = 1
        total = 0
        for weight in weights:
            total += weight
            if total > capacity:  # too heavy, wait for the next day
                total = weight
                days += 1
                if days > D:  # cannot ship within D days
                    return False
        return True
```

Given a capacity, this function greedbily checks to see if it's possible to send all packages in D days. 

Now the problem is about finding the right capacity that will allow us to ship all of our items in D days. 

We use binary search to find the right capacity.

Our starting value is max\(weights\), because if it wasn't we wouldn't be able to ship the heaviest package. I.E. we wouldn't be able to ship all the packages.

Our ending value for search is the sum of all the weights. If we can send a package out in sum\(weights\), that means we can send all packages out on the same day.

```python
class Solution:
    def shipWithinDays(self, weights: List[int], D: int) -> int:
        def feasible(capacity) -> bool:
            days = 1
            total = 0
            for weight in weights:
                total += weight
                if total > capacity:  # too heavy, wait for the next day
                    total = weight
                    days += 1
                    if days > D:  # cannot ship within D days
                        return False
            return True

        left, right = max(weights), sum(weights)
        while left < right:
            mid = left + (right - left) // 2
            if feasible(mid):
                right = mid
            else:
                left = mid + 1
        return left
```

In total, this algorithm required 2 things:

* A function to check if a certain capacity is possible \(our condition\)
* Understanding that our range is from max\(weights\) to sum\(weights\).

We then, using binary search, half our search space each time to find the right one that works \(if it exists\).
{% endtab %}
{% endtabs %}



