# Binary Tree Inorder Traversal

{% hint style="info" %}
[https://leetcode.com/problems/binary-tree-inorder-traversal/](https://leetcode.com/problems/binary-tree-inorder-traversal/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the `root` of a binary tree, return _the inorder traversal of its nodes' values_.

**Example 1:**![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```text
Input: root = [1,null,2,3]
Output: [1,3,2]
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
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        to_ret = []
        def inorder(root):
            if not root:
                return
            inorder(root.left)
            to_ret.append(root.val)
            inorder(root.right)
        inorder(root)
        return to_ret
```
{% endtab %}
{% endtabs %}

