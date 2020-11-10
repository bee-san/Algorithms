# Ugly Number 3

{% hint style="info" %}
[https://leetcode.com/problems/ugly-number-iii/](https://leetcode.com/problems/ugly-number-iii/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Write a program to find the `n`-th ugly number.

Ugly numbers are **positive integers** which are divisible by `a` **or** `b` **or** `c`.

**Example 1:**

```text
Input: n = 3, a = 2, b = 3, c = 5
Output: 4
Explanation: The ugly numbers are 2, 3, 4, 5, 6, 8, 9, 10... The 3rd is 4.
```
{% endtab %}

{% tab title="Answer" %}
Nothing special. Still finding the Kth-Smallest. We need to design an `enough` function, given an input `num`, determine whether there are at least n ugly numbers less than or equal to `num`. Since `a` might be a multiple of `b` or `c`, or the other way round, we need the help of greatest common divisor to avoid counting duplicate numbers.

```python
def nthUglyNumber(n: int, a: int, b: int, c: int) -> int:
    def enough(num) -> bool:
        total = mid//a + mid//b + mid//c - mid//ab - mid//ac - mid//bc + mid//abc
        return total >= n

    ab = a * b // math.gcd(a, b)
    ac = a * c // math.gcd(a, c)
    bc = b * c // math.gcd(b, c)
    abc = a * bc // math.gcd(a, bc)
    left, right = 1, 10 ** 10
    while left < right:
        mid = left + (right - left) // 2
        if enough(mid):
            right = mid
        else:
            left = mid + 1
    return left
```
{% endtab %}
{% endtabs %}

