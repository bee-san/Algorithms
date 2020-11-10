# Sort Array by Parity

{% hint style="info" %}
[https://leetcode.com/problems/sort-array-by-parity/](https://leetcode.com/problems/sort-array-by-parity/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `A` of non-negative integers, return an array consisting of all the even elements of `A`, followed by all the odd elements of `A`.

You may return any answer array that satisfies this condition.

**Example 1:**

```text
Input: [3,1,2,4]
Output: [2,4,3,1]
The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```
{% endtab %}

{% tab title="Answer" %}
We can sort using the sort function.

```python
class Solution(object):
    def sortArrayByParity(self, A):
        A.sort(key = lambda x: x % 2)
        return A
```

Or we can write all the even elements first, then write all the odd elements.

```python
class Solution(object):
    def sortArrayByParity(self, A):
        return ([x for x in A if x % 2 == 0] +
                [x for x in A if x % 2 == 1])
```

**Approach 3: In-Place**

**Intuition**

If we want to do the sort in-place, we can use quicksort, a standard textbook algorithm.

**Algorithm**

We'll maintain two pointers `i` and `j`. The loop invariant is everything below `i` has parity `0` \(ie. `A[k] % 2 == 0` when `k < i`\), and everything above `j` has parity `1`.

Then, there are 4 cases for `(A[i] % 2, A[j] % 2)`:

* If it is `(0, 1)`, then everything is correct: `i++` and `j--`.
* If it is `(1, 0)`, we swap them so they are correct, then continue.
* If it is `(0, 0)`, only the `i` place is correct, so we `i++` and continue.
* If it is `(1, 1)`, only the `j` place is correct, so we `j--` and continue.

Throughout all 4 cases, the loop invariant is maintained, and `j-i` is getting smaller. So eventually we will be done with the array sorted as desired.

```python
class Solution(object):
    def sortArrayByParity(self, A):
        i, j = 0, len(A) - 1
        while i < j:
            if A[i] % 2 > A[j] % 2:
                A[i], A[j] = A[j], A[i]

            if A[i] % 2 == 0: i += 1
            if A[j] % 2 == 1: j -= 1

        return A
```

from [here](https://leetcode.com/problems/sort-array-by-parity/solution/).
{% endtab %}
{% endtabs %}



