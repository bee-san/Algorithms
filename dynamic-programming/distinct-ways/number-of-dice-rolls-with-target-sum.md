# Number of Dice Rolls with Target Sum

{% hint style="info" %}
[https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You have `d` dice, and each die has `f` faces numbered `1, 2, ..., f`.

Return the number of possible ways \(out of `fd` total ways\) **modulo `10^9 + 7`** to roll the dice so the sum of the face up numbers equals `target`.

```text
Input: d = 1, f = 6, target = 3
Output: 1
Explanation: 
You throw one die with 6 faces.  There is only one way to get a sum of 3.
```
{% endtab %}

{% tab title="Answer" %}
From [here](https://leetcode.com/problems/number-of-dice-rolls-with-target-sum/discuss/355894/Python-DP-with-memoization-explained). 

Let's start off by examining it with 1 dice.

If we have 1 dice, and our target 1 &lt;= N &lt;= 6 then we will only ever have 1 way.

Now, what if we introduce 2 die?

Because a dice can only be rolled once, we'd want to use something multi-diimensional such as:

```text
[ [1, 2, 3, 4, 5, 6], [1, 2, 3, 4, 5, 6] ]
```

We've actually seen something like this before. When we have 2 dice with 6 faces and a target 12 that means that if we know the value of dice1, we can work out the value for dice2:

$$
12  - 6 = 6
$$

* Target is 12
* Dice1 is 6
* Dice2 **must** be 6.

Now, let's go one step further. Let's see X number of die.

Our target value is 18. We have X die. Each die has 6 faces.

Assume we define our function as `dp(num_dice, num_faces, target_value)`.

We will roll one dice and see how it changes things.

* Die = 1. The remaining X dice must sum to 18 - 1 = **17** **ways**. This can happen with `dp(x,  6, 17)`.
* Die = 2. The remaining dice must sum to 18 - 2 = **16 ways.** This can happen `dp(x, 6, 16)` ways.
* Die = 3. The remaining dice must sum to 18 - 3 = **15 ways.** This can happen `dp(x, 6, 15)` ways.
* Die = 4.The remaining dice must sum to 18 - 4 = 14 ways. This can happen `dp(x, 6, 14)` ways.
* Die = 5, The remaining dice must sum to 18 - 5 = 13 ways. This can happen `dp(x, 6, 13)` ways.
* Die = 6.The remaining dice must sum to 18 - 6 = 12 ways. This can happen `dp(x, 6, 12)` ways.

$$
dp(x, 6, 18) = dp(x, 6, 17) + dp(x, 6, 16) + dp(x, 6, 15) + dp(x, 6, 14) + dp(x, 6, 13) + dp(x, 6, 12)
$$

We sum up all these 6 cases to arrive at our We sum up the solutions these 6 cases to arrive at our result. Of course, each of these cases branches off into 6 cases of its own, and the recursion only resolves when d=0. The handling of this base case is explained below.. 

 The general relation is:

**dp**\(d, f, target\) = **dp**\(d-1, f, target-1\) + **dp**\(d-1, f, target-2\) + ... + **dp**\(d-1, f, target-f\)

The base case occurs when `d` = 0. We can make `target=0` with 0 dice, but nothing else.  
So **dp**\(0, f, t\) = 0 iff `t` != 0, and **dp**\(0, f, 0\) = 1.

Use memoization to avoid repeated calculations and don't conisider negative targets.

```python
class Solution:
    def numRollsToTarget(self, d: int, f: int, target: int) -> int:
        memo = {}
        def dp(d, target):
            if d == 0:
                return 0 if target > 0 else 1
            if (d, target) in memo:
                return memo[(d, target)]
            to_return = 0
            for k in range(max(0, target-f), target):
                to_return += dp(d-1, k)
            memo[(d, target)] = to_return
            return to_return
        return dp(d, target) % (10**9 + 7)
```
{% endtab %}
{% endtabs %}

