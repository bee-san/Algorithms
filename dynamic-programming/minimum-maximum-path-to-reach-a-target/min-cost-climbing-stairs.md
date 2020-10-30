# Min Cost Climbing Stairs

{% hint style="info" %}
[https://leetcode.com/problems/min-cost-climbing-stairs/](https://leetcode.com/problems/min-cost-climbing-stairs/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
On a staircase, the `i`-th step has some non-negative cost `cost[i]` assigned \(0 indexed\).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        for i in range(2, len(cost)):
            cost[i] = min(cost[i] + cost[i - 1], cost[i] + cost[i - 2])
        return min(cost[-1], cost[-2])
```

The first 2 steps are our basecases, from there every value up to the length of the cost we work out the value.

The value is the minimum of:   


* The current step added to the step immediately before it \(cost\[i - 1\]\)
* The current step added to the step 2 before it \(cost\[i - 2\]\)

This is Fibonacci sequence.

We return whichever one is minimum between \[-2\] and \[-1\]. Since we can go up 2 steps, we can end at \[-2\] instead of \[-1\] depending on which is minimum.
{% endtab %}
{% endtabs %}

