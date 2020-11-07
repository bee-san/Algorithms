# Reverse a Linked List

{% hint style="info" %}
[https://leetcode.com/problems/reverse-linked-list/](https://leetcode.com/problems/reverse-linked-list/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Reverse a singly linked list.

**Example:**

```text
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
{% endtab %}

{% tab title="Answer" %}
We swap the head with the previous node, which reverses the list.

```python
def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        while head:
            # swaps nodes
            curr = head
            head = head.next
            curr.next = prev
            
            # stores the list
            prev = curr
        return prev
```

We can also do this in 3 lines in Python:

```python
def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        cur, prev = head, None
        while cur:
            cur.next, prev, cur = prev, cur, cur.next
        return prev
```

Using Tuple Unpacking. Or we can do it recursively:

```python
def reverseList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        node = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return node
```
{% endtab %}
{% endtabs %}

