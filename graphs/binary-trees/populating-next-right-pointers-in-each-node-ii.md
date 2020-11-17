# Populating Next Right Pointers in Each Node II

{% hint style="info" %}
[https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree

```text
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

**Follow up:**

* You may only use constant extra space.
* Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

```text
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```
{% endtab %}

{% tab title="Answer" %}
From [here](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/discuss/37824/AC-Python-O%281%29-space-solution-12-lines-and-easy-to-understand).

The algorithm is a BFS or level order traversal. We go through the tree level by level. node is the pointer in the parent level, tail is the tail pointer in the child level. The parent level can be view as a singly linked list or queue, which we can traversal easily with a pointer. Connect the tail with every one of the possible nodes in child level, update it only if the connected node is not nil. Do this one level by one level. The whole thing is quite straightforward.

```python
def connect(self, node):
    tail = dummy = Node(0)
    while node:
        tail.next = node.left
        if tail.next:
            tail = tail.next
        tail.next = node.right
        if tail.next:
            tail = tail.next
        node = node.next
        if not node:
            tail = dummy
            node = dummy.next
```
{% endtab %}
{% endtabs %}

