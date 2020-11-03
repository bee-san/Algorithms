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

{% tab title="Answer" %}
```python
class Solution:
    def numSquares(self, n: int) -> int:
        
```

The problem starts off with basecases. 

* When n is 0, we should return 0.

We should then build an array up to n log\(n\). This is because any number past log\(n\) cannot be a perfect divisor of `n`.

In this array we calculate every possible value up to the target. The minimum for `n` is either:

* the minimum for the number before, i\[j\].
{% endtab %}
{% endtabs %}

```text
def numSquares(n):
	dp = [0] + [float('inf')]*n
	for i in range(1, n+1):
		for j in range(1, int(i**0.5) + 1):
			dp[i] = min(dp[i-j*j]) + 1
	return dp[n]
```

