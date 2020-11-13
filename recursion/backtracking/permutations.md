# Permutations

{% hint style="info" %}
[https://leetcode.com/problems/permutations/](https://leetcode.com/problems/permutations/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```text
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
{% endtab %}

{% tab title="Answer" %}
{% embed url="https://www.youtube.com/watch?v=KukNnoN-SoY" %}

![](../../.gitbook/assets/image%20%2839%29.png)

Let's build the recursion tree, stole from this video!

![](../../.gitbook/assets/image%20%2841%29.png)

We remove 1 from our possible numbers and add it to our array.

Every iteration \(i = 0\) we iterate over the array.

Now we iterate over \[2, 3\].

![](../../.gitbook/assets/image%20%2838%29.png)

Now we move 2 from our array to the answer set.

![](../../.gitbook/assets/image%20%2840%29.png)

Now we push 0.

Our array is now empty, that's our base case. We can return from this function call. But before we do that we want to push this into our answers array.

![](../../.gitbook/assets/image%20%2837%29.png)
{% endtab %}
{% endtabs %}

