# Middle of the Linked List

{% hint style="info" %}
[https://leetcode.com/problems/middle-of-the-linked-list/submissions/](https://leetcode.com/problems/middle-of-the-linked-list/submissions/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a non-empty, singly linked list with head node `head`, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

```text
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```
{% endtab %}

{% tab title="Answer" %}
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        tmp = head
        while tmp and tmp.next:
            head = head.next
            tmp = tmp.next.next
        return head
```

We need two pointers, one is head with one step each iteration, and the other is tmp with two steps each iteration. So when the tmp reaches the end of the list, the head just reaches the half of it, which is exactly what we want.

And one thing needs to be considered additionaly is that the number of the node can be odd and even, which may affect the termination condition of the iteration. To solve this, my idea is to try the algorithm in some small set of the examples, like the examples provided by the official. And you will find that if the tmp reaches Null or tmp.next reaches Null, the head is the result.

Explanation from [here](https://leetcode.com/problems/middle-of-the-linked-list/discuss/154696/Python-two-pointer-extremely-simple-with-explaination).

O\(n\) time and O\(1\) space.

On BinarySearch this is 100% fastest.

![](../../.gitbook/assets/image%20%2825%29.png)
{% endtab %}
{% endtabs %}

