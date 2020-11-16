# Symmetric Tree

{% hint style="info" %}
[https://leetcode.com/problems/symmetric-tree/](https://leetcode.com/problems/symmetric-tree/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree, check whether it is a mirror of itself \(ie, symmetric around its center\).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```text
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```text
    1
   / \
  2   2
   \   \
   3    3
```
{% endtab %}

{% tab title="Answer" %}
A symmetric tree means that every subtree is equal to eachother.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def symmetric(n1, n2):        
            if not n1 and not n2:
                return True
            if (not n1 and n2) or (not n2 and n1):
                return False
            return n1.val == n2.val and symmetric(n1.left, n2.right) and symmetric(n1.right, n2.left)
           
        return symmetric(root, root)
```

We can solve this by recursing through the tree. If the val of the 2 nodes are equal, then we are good at that specific part.

And then we recurse. If the left and right subtrees are the same, and the right and left subtrees are the same, for every value we return True.
{% endtab %}
{% endtabs %}

