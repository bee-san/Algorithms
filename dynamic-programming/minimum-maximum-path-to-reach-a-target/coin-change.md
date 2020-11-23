# Coin Change

{% hint style="info" %}
[https://leetcode.com/problems/coin-change/](https://leetcode.com/problems/coin-change/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

```text
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int: 
        
        dp = [float("inf")] * (amount + 1)
        
        dp[0] = 0
        
        for y in range(1, amount + 1):
            for coin in coins:
                
                if y - coin < 0:
                    continue
                
                dp[y] = min(dp[y], dp[y - coin] + 1)
                
        if dp[-1] == float("inf"):
            return -1
        
        return dp[-1]
```

We generate a list the size of amount + 1, and set the first element to 0. We can make 0 coins with 0.

Then we calculate the minimum number of coins for each amount up to the target. 

We first check to see if our current amount - the denomination we are checking is below 0. If it is, we cannot use this coin for change so we move onto the next one.

If it's not, the change is either:

* The current amount \(which in first loop is infinite, but in future loops will be different\)
* The current amount take away the denomination + 1. The fewest amount to make y coins, with whatever coin we just took. **We want to figure out whatever the best amount it is to make that amount in our dp array. `y - coin` is the best amount to make that amount.** The 1 is because we add one single coin.

If our last value \(the target amount\) is infinite, we return -1 \(as we couldn't change for that amount optimally\). Else we return the last value.  
  
Our runtime is O\(nm\) where n is our amount and m is the coins we are given. Space O\(n\) where n is how big our amount is.  
**Small optimisation**  
We can sort the array, and if our current coin is larger than the amount we break and return as there's no point in going through bigger and bigger coins.

Also see my answer here:

{% embed url="https://binarysearch.com/problems/Making-Change-Sequel/editorials/3021912" %}



{% embed url="https://www.youtube.com/watch?v=1R0\_7HqNaW0" %}
{% endtab %}
{% endtabs %}

