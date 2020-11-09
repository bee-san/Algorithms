# Add Two Numbers 2

{% hint style="info" %}
[https://leetcode.com/problems/add-two-numbers-ii/](https://leetcode.com/problems/add-two-numbers-ii/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**  
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```text
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```
{% endtab %}

{% tab title="Answer" %}
We can cheat by turning the numbers into strings, adding them together and then creating a new linked list.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        v1 = str("")
        while l1:
            v1 = v1 + str(l1.val)
            l1 = l1.next
        
        v2 = ""
        while l2:
            v2 = v2 + str(l2.val)
            l2 = l2.next
        
        v3 = str(int(v1) + int(v2))
        
        head = ListNode(int(v3[0]))
        res = head
        
        for i in range(1, len(v3)):
            head.next = ListNode(int(v3[i]))
            head = head.next
            
        return res
```

Your interviewer may be impressed with your ingenuity, but shortly after they'll ask you to do is another way.

The 2nd way is to use a stack.

We append our values to stacks.

```python
class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # Use two stacks to store the number
        stack1 = []
        stack2 = []
        ptr = l1
        while l1:
            stack1.append(l1.val)
            l1 = l1.next
        ptr = l2
        while l2:
            stack2.append(l2.val)
            l2 = l2.next
```

We then iterate through the stacks.

```python
        carry = 0
        result = []
        head = ListNode(-1)
        while stack1 or stack2:
            if not stack1:
                val = stack2.pop()
            elif not stack2:
                val = stack1.pop()
            else:
                val = stack1.pop() + stack2.pop()  
```

We divide and calculate the modulus using `divmod`:

```python
carry, val = divmod(carry + val, 10)
```

We now know what the carry is, as well as if we have carry.

We then place this in our current list node, create a new list node and go to the next one.

```python
            head.val = val
            temp = head
            head = ListNode(-1)
            head.next = temp
```

We then either return the 2nd to last node if our list is complete, or the last node if we had to carry.

```python
        if carry: head.val = carry
        return head if head.val != -1 else head.next 
```

All together we get:

```python
class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # Use two stacks to store the number
        stack1 = []
        stack2 = []
        ptr = l1
        while l1:
            stack1.append(l1.val)
            l1 = l1.next
        ptr = l2
        while l2:
            stack2.append(l2.val)
            l2 = l2.next
            
        carry = 0
        result = []
        head = ListNode(-1)
        while stack1 or stack2:
            if not stack1:
                val = stack2.pop()
            elif not stack2:
                val = stack1.pop()
            else:
                val = stack1.pop() + stack2.pop()    
            carry, val = divmod(carry + val, 10)
            head.val = val
            temp = head
            head = ListNode(-1)
            head.next = temp
        if carry: head.val = carry
        return head if head.val != -1 else head.next 
```
{% endtab %}
{% endtabs %}

