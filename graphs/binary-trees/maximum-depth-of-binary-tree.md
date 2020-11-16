# Maximum Depth of Binary Tree

{% hint style="info" %}
[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Note:** A leaf is a node with no children.

**Example:**

Given binary tree `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.
{% endtab %}

{% tab title="Answer" %}
The easiest way to do it is by keeping an array of our lengths:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        lengths = []
        def dfs(root, length = 0):
            if not root:
                lengths.append(length)
                return 
            length += 1
            dfs(root.left, length)
            dfs(root.right, length)
        dfs(root)
        return max(lengths)
```

The intuitive way is to recurse:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        def dfs(root, depth = 0):
            return max(dfs(root.left, depth + 1), dfs(root.right, depth + 1)) if root  else depth
        return dfs(root)
```

We return the maximum of either the left or right, and we error check with the one line if statement.
{% endtab %}
{% endtabs %}

