# Lowest Common Ancestor of a Binary Tree

{% hint style="info" %}
[https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants \(where we allow **a node to be a descendant of itself**\).”

**Example 1:**![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```text
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```text
Input: root = [1,2], p = 1, q = 2
Output: 1
```
{% endtab %}

{% tab title="Answer" %}
{% embed url="https://www.youtube.com/watch?v=py3R23aAPCA" %}

![](../../.gitbook/assets/image%20%2867%29.png)

Find the LCA. The black coloured one is the lowest common ancestor of X and Y.

The first common ancestor we see going from bottom to top is the lowest common ancestor.

![](../../.gitbook/assets/image%20%2860%29.png)

X is the lowest common ancestor of X and Y. That's because X can be an ancestor of itself.

Only focus on a single node. What needs to happen at a single node for me to solve the problem? One node is a function call.

![](../../.gitbook/assets/image%20%2864%29.png)

![](../../.gitbook/assets/image%20%2859%29.png)

Our right, and our left \(unique instances, no duplicates\). What we know is that what we are holding is a common ancestor. Is it the lowest common ancestor? It has to be.

Our recursion is going bottom up.

If we find a node left, and find a node right, this root **must** be the lowest common ancestor.

What if we find 1 on the left, and nothing on the right?

![](../../.gitbook/assets/image%20%2856%29.png)

It cannot be! 

From root, we can reach Y. 

If we found something on the right, but nothing on the left. We return the x or the y back upwards saying "we can reach this value, from this node."

Each call represents asking "what is the lowest common ancestor from this node?"

![](../../.gitbook/assets/image%20%2868%29.png)

When we have Null as the root, we can't find the LCA.

![](../../.gitbook/assets/image%20%2862%29.png)

If root is either of the values, we return root.

![](../../.gitbook/assets/image%20%2861%29.png)

Else, we search:

![](../../.gitbook/assets/image%20%2863%29.png)

What we need to do is look back to our cases. If we get nothing on the left, return the right.

If we get nothing on the right, return what we get on the left.

![](../../.gitbook/assets/image%20%2855%29.png)

So we just return ourselves at the end.

![](../../.gitbook/assets/image%20%2857%29.png)

We drill down, and come back up \(because of recursion\).

If we find both and we are the LCA, we return ourselves to our parent who says "left and right search" and a result, the node that was the LCA keeps getting passed upwards until it gets returned as the LCA.

The time is O\(h\) for height, and o\(h\) for space.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root:
            return None
        if root.val == p.val or root.val == q.val:
            return root
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        if left == None:
            return right
        if right == None:
            return left
        return root
```
{% endtab %}
{% endtabs %}



