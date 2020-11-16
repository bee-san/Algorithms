# Binary Tree Postorder Traversal

{% hint style="info" %}
[https://leetcode.com/problems/binary-tree-postorder-traversal/](https://leetcode.com/problems/binary-tree-postorder-traversal/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the `root` of a binary tree, return _the postorder traversal of its nodes' values_.

**Example 1:**![](https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg)

```text
Input: root = [1,null,2,3]
Output: [3,2,1]
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
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        to_ret = []
        def postorder(root):
            if not root:
                return
            postorder(root.left)
            postorder(root.right)
            to_ret.append(root.val)
        postorder(root)
        return to_ret
```
{% endtab %}
{% endtabs %}

