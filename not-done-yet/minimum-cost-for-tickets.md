# Minimum Cost For Tickets

{% hint style="info" %}
[https://leetcode.com/problems/minimum-cost-for-tickets/](https://leetcode.com/problems/minimum-cost-for-tickets/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
In a country popular for train travel, you have planned some train travelling one year in advance.  The days of the year that you will travel is given as an array `days`.  Each day is an integer from `1` to `365`.

Train tickets are sold in 3 different ways:

* a 1-day pass is sold for `costs[0]` dollars;
* a 7-day pass is sold for `costs[1]` dollars;
* a 30-day pass is sold for `costs[2]` dollars.

The passes allow that many days of consecutive travel.  For example, if we get a 7-day pass on day 2, then we can travel for 7 days: day 2, 3, 4, 5, 6, 7, and 8.

Return the minimum number of dollars you need to travel every day in the given list of `days`.

```text
Input: days = [1,4,6,7,8,20], costs = [2,7,15]
Output: 11
Explanation: 
For example, here is one way to buy passes that lets you travel your travel plan:
On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.
On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.
On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.
In total you spent $11 and covered all the days of your travel.
```
{% endtab %}

{% tab title="Answer" %}
Let's see an example of this. Given the array:

```text
days = [1, 4, 6, 7, 8, 20]
```

And the ticket costs:

```text
costs = [2, 7, 15]
```

We want to find out the minimum cost to travel everyday in the given list. Essentially, saving us money.

Costs is:

```text
cost[0] = 1 day
cost[1] = 7 days
costs[2] = 30 days
```

Let's try to build this into a recurrence.

**Base case**

1 day = cost\[0\]

**Divide & Conquer**

Everyday after this is either the minimum cost of the previous days, or the current ticket.

So if we are at 7 days, our cost will either be:

* Day 6's ticket \(assuming it covers that day\)
* Day 7's cost\[1\] ticket

While calculating the min, we need to make sure our ticket does not exceed the days.   
  
We can visualise this with a table:  
  


This methodology quickly falls apart, as our recurrence will look like:

* Previous days ticket \(assuming the day is covered\)
* Greedy search for the ticket  [https://leetcode.com/problems/minimum-cost-for-tickets/discuss/630868/explanation-from-someone-who-took-2-hours-to-solve](https://leetcode.com/problems/minimum-cost-for-tickets/discuss/630868/explanation-from-someone-who-took-2-hours-to-solve)
{% endtab %}
{% endtabs %}





