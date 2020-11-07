# Add Two Numbers

{% hint style="info" %}
[https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
{% endtab %}

{% tab title="Answer" %}
Let's examine this problem.

![](../.gitbook/assets/image%20%2817%29.png)

We'll build a 3rd linked list for our case.

Now let's add the first two nodes.

$$
2+5 = 7
$$

![](../.gitbook/assets/image%20%2818%29.png)

Okay, now the next pair.

$$
4 + 6 = 10
$$

![](../.gitbook/assets/image%20%2816%29.png)

To calculate the carry, we do:

$$
10 \;mod\; 10 =0
$$

This means our nodes current value is 0, and our carry is 1.

We then build the next node.

![](../.gitbook/assets/image%20%2821%29.png)

If we carry on our last node, we should continue until we no longer have carry.

That means we should loop:

```python
while l1.head and l2.head and carry
```

Then we add together the 2 values, but don't insert into our new linked list.

```python
val = l1.val + l2.val
```

We calculate if it'll carry:

```python
if val % 10 == 0
```
{% endtab %}
{% endtabs %}







