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
{% embed url="https://www.youtube.com/watch?v=aM4Iv7eEr2o" %}



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

We want to make sure our list nodes exist. As in, if we have 4 digits in l1 and 6 digits in l2 we need to make sure we can deal with these edge cases.

```python
if l1:
    carry += l1.val
    l1 = l1.next
```

And we do this for l2  too.

And then the value for the next node is the last digit. So to calculate carry we divide by 10. To get the remaining value \(the last digit of the number after carry\) we use modulus.

```python
curr.next = ListNode(carry % 10)
```

Now we need to clean up. We move our curr pointer to next and calculate the carry for the next value.

If our carry is below 10, because we are using floor division we will get 0. Which means we do not have to worry about this edge case, as our code will only add a carry if needed.

Using modulus, we also don't have to worry about it being under 10. Since `6 % 10 = 6.`

```python
def addTwoNumbers(self, l1, l2):
    dummy = cur = ListNode(0)
    carry = 0
    while l1 or l2 or carry:
        if l1:
            carry += l1.val
            l1 = l1.next
        if l2:
            carry += l2.val
            l2 = l2.next
        cur.next = ListNode(carry%10)
        cur = cur.next
        carry //= 10
    return dummy.next
```
{% endtab %}
{% endtabs %}







