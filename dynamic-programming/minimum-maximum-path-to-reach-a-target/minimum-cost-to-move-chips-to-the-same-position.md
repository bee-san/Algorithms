# Minimum Cost to Move Chips to The Same Position

{% hint style="info" %}
[https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/](https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
We have `n` chips, where the position of the `ith` chip is `position[i]`.

We need to move all the chips to **the same position**. In one step, we can change the position of the `ith` chip from `position[i]` to:

* `position[i] + 2` or `position[i] - 2` with `cost = 0`.
* `position[i] + 1` or `position[i] - 1` with `cost = 1`.

Return _the minimum cost_ needed to move all the chips to the same position.

![](../../.gitbook/assets/image%20%285%29.png)

```text
Input: position = [1,2,3]
Output: 1
Explanation: First step: Move the chip at position 3 to position 1 with cost = 0.
Second step: Move the chip at position 2 to position 1 with cost = 1.
Total cost is 1.
```
{% endtab %}

{% tab title="Answer" %}
This is a dynamic programming problem, because it asks us to find the combination that minimises the cost.

But, do we really need dynamic programming? Let's try a dumb method to see if it works.

Occam's razor states:

> The simplest solution is always the best.

* We can move a coin from one side to the other for 0 cost.
* To move a coin one over, it'll cost 1.

![](../../.gitbook/assets/image%20%2810%29.png)

We want to match 2 things:

* Less movements, so we want to try to move to a slot with more coins by default.
* Movements from edge to edge are cheaper.

![](../../.gitbook/assets/image%20%289%29.png)

In this instance, we want to move all the coins to one side. 

We have 1 cost for moving the middle to the other slots, and no cost for moving the outer edge to another outer edge.

This means our cost is 1.

![](../../.gitbook/assets/image%20%286%29.png)

But we don't always want to focus on the edge. In this case, it is better to take the cost of 1 to move to the middle.

![](../../.gitbook/assets/image%20%287%29.png)

It's free to move a coin from an odd number to another odd number. It is free to move a coin from an even number to another even number.  
  
Therefore we want to calculate whether it is cheaper to move all the odd coins to even, or all the even coins to odd.   
  
Since the cost is 1, we only need to calculate how many odd or even coins we have.

```python
class Solution:
    def minCostToMoveChips(self, position: List[int]) -> int:
        even = 0
        odd = 0
        for coin in position:
            if coin % 2 == 0:
                even += 1
            else:
                odd += 1
        return min(even, odd)
```

Hope you don't mind me including this here! This seems like a dynamic programming problem, but when we look at it and take into account Occam's Razor we see that it's not.

This is an important step. This problem is defined perfectly for DP, and perfectly for the minimum path to reach a target. But it's not if we examine the problem closer!

Always come up with a bruteforce solution and try to solve it first, if you have the time. Never go in thinking "this is dynamic programming" when it may not be. 
{% endtab %}
{% endtabs %}



