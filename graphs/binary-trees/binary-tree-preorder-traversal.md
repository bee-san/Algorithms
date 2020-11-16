# Binary Tree Preorder Traversal

{% hint style="info" %}
[https://leetcode.com/problems/binary-tree-preorder-traversal/](https://leetcode.com/problems/binary-tree-preorder-traversal/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.

**Example 1:**![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```text
Input: root = [1,null,2,3]
Output: [1,2,3]
```
{% endtab %}

{% tab title="Answer" %}
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        to_ret = []
        def preorder(root):
            if not root:
                return
            to_ret.append(root.val)
            preorder(root.left)
            preorder(root.right)
        preorder(root)
        return to_ret
```

If the root node does not exist, return nothing.

Else perform preorder by:

* Appending the value
* Left recurse
* Right recurse
{% endtab %}
{% endtabs %}

