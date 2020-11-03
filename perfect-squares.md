# Perfect Squares

{% hint style="info" %}
[https://leetcode.com/problems/perfect-squares/](https://leetcode.com/problems/perfect-squares/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a positive integer n, find the least number of perfect square numbers \(for example, `1, 4, 9, 16, ...`\) which sum to n.

```text
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

  
{% endtab %}

{% tab title="Hint" %}
We've seen accessing the last element, or the second to last element in our DP array to perform the recursive step.

What if we wanted to access an element based on a mathematical calculation?
{% endtab %}

{% tab title="Answer" %}
Our base case is that 0 == 0:

* dp\[0\] = 0

Now, how do we calculate the recurrence?

Firstly, we need to calculate all possible square numbers up to `j`. j is not our current index, since any number past half of our index squared will be over it. For example, take 4. Half of 4 is 2. Any number over 2 squared \(such as 3^2\) will not be equal to 4.

We can use a mathematical calculation for this:

$$
j = int(i**0.5) + 1
$$

To the power of 0.5 is the same as square rooting.

We add 1 to deal with indices and getting the right candidate. If the answer for 4 is 2^2, the answer for 5 will not also be 2^2. So we add one.

There are multiple squares that add up to the index, so we need to select the minimum out of this list. 

The dynamic programming comes into play because we do not need to recalculate square numbers. If our number is 4, and our `j` value is 2 we can use the minimum for `2.`
{% endtab %}
{% endtabs %}

```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [0] + [float("inf")] * n
        for i in range(1, n+1):
            dp[i] = min(dp[i-j*j] for j in range(1, int(i**0.5) + 1)) + 1
        return dp[n]
```

