# KoKo Eating Banana

{% hint style="info" %}
[https://leetcode.com/problems/koko-eating-bananas/](https://leetcode.com/problems/koko-eating-bananas/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}


Koko loves to eat bananas.  There are `N` piles of bananas, the `i`-th pile has `piles[i]` bananas.  The guards have gone and will come back in `H` hours.

Koko can decide her bananas-per-hour eating speed of `K`.  Each hour, she chooses some pile of bananas, and eats K bananas from that pile.  If the pile has less than `K` bananas, she eats all of them instead, and won't eat any more bananas during this hour.

Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back.

Return the minimum integer `K` such that she can eat all the bananas within `H` hours.

**Example 1:**

```text
Input: piles = [3,6,7,11], H = 8
Output: 4
```
{% endtab %}

{% tab title="Answer" %}
Very similar to LC 1011 and LC 410 mentioned above. Let's design a `feasible` function, given an input `speed`, determine whether Koko can finish all bananas within `H` hours with hourly eating speed `speed`. Obviously, the lower bound of the search space is 1, and upper bound is `max(piles)`, because Koko can only choose one pile of bananas to eat every hour.

```python
def minEatingSpeed(piles: List[int], H: int) -> int:
    def feasible(speed) -> bool:
        # return sum(math.ceil(pile / speed) for pile in piles) <= H  # slower        
        return sum((pile - 1) / speed + 1 for pile in piles) <= H  # faster

    left, right = 1, max(piles)
    while left < right:
        mid = left  + (right - left) // 2
        if feasible(mid):
            right = mid
        else:
            left = mid + 1
    return left
```
{% endtab %}
{% endtabs %}

