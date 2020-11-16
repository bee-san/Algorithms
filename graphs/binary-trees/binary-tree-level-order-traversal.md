# Binary Tree Level Order Traversal

{% hint style="info" %}
[https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree, return the level order traversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,  


```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:  


```text
[
  [3],
  [9,20],
  [15,7]
]
```
{% endtab %}

{% tab title="Answer" %}
Breadth first search \(level order traversal\) is implemented using a queue.

Since binary trees either have a left or right node, we can keep track of this using 2 lists.

* temp1 == values of all nodes at that level
* temp2 == left & right nodes

For every node in our right child, we append to temp1 the values we come across.

We then append to temp2 the left and right nodes.

And then we recourse on temp2, after appending temp1 to our return list.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]: 
        to_ret = []
        
        def bfs(level):
            temp1, temp2 = [],[]
            if not level or not level[0]:
                return
            for node in level:
                temp1.append(node.val)
                if node.left:
                    temp2.append(node.left)
                if node.right:
                    temp2.append(node.right)    
            to_ret.append(temp1)
            bfs(temp2)
            
        
        bfs([root])
        return to_ret
```
{% endtab %}
{% endtabs %}

