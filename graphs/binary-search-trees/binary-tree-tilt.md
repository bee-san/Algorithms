# Binary Tree Tilt

{% hint style="info" %}
[https://leetcode.com/problems/binary-tree-tilt/](https://leetcode.com/problems/binary-tree-tilt/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the `root` of a binary tree, return _the sum of every tree node's **tilt**._

The **tilt** of a tree node is the **absolute difference** between the sum of all left subtree node **values** and all right subtree node **values**. If a node does not have a left child, then the sum of the left subtree node **values** is treated as `0`. The rule is similar if there the node does not have a right child.

![](../../.gitbook/assets/image%20%2824%29.png)

```text
Input: root = [1,2,3]
Output: 1
Explanation: 
Tilt of node 2 : |0-0| = 0 (no children)
Tilt of node 3 : |0-0| = 0 (no children)
Tile of node 1 : |2-3| = 1 (left subtree is just left child, so sum is 2; right subtree is just right child, so sum is 3)
Sum of every tilt : 0 + 0 + 1 = 1
```
{% endtab %}

{% tab title="Answer" %}
This sounds like DFS. So let's start trying to recurse.  


Our base case is that if the root is None, we return

```text
if not root:
    return 0
```

And then we want to recurse both left and right trees.

```python
        right_sum = self.helper(root.right)
        left_sum = self.helper(root.left)
```

While doing this, we want to sum each side. We can do that by storing them in these variables. And then we calculate the tilt:

```text
        tilt = abs(left_sum - right_sum)
        self.total_sum += tilt
```

Finally, when we have reached a leaf node we want it to return the sums of either side added to the current value. 

```text
    return left_sum + right_sum + root.val
```

Thus our solution is:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findTilt(self, root: TreeNode) -> int:
        self.total_sum = 0
        self.helper(root)
        return self.total_sum
    
    def helper(self, root):
        if not root:
            return 0
        right_sum = self.helper(root.right)
        left_sum = self.helper(root.left)
        tilt = abs(left_sum - right_sum)
        self.total_sum += tilt
        
        return left_sum + right_sum + root.val
```
{% endtab %}
{% endtabs %}

