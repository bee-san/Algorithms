# Counting Maximal Value Roots in Binary Tree

{% hint style="info" %}
[https://binarysearch.com/problems/Counting-Maximal-Value-Roots-in-Binary-Tree](https://binarysearch.com/problems/Counting-Maximal-Value-Roots-in-Binary-Tree)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a binary tree `root`, count and return the number of nodes where its value is greater than or equal to the values of all of its descendants.

For example, given

```text
   6
  / \
 3   2
    / \
   6   4
```

Return `4` since all nodes except for `2` meet the criteria.

#### Example 1

**Input**

```text
root = [6, [3, null, null], [2, [6, null, null], [4, null, null]]]
```

**Output**

```text
4
```
{% endtab %}

{% tab title="Answer" %}
```python
# class Tree:
#     def __init__(self, val, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def solve(self, root):
        count = 0

        def dfs(root):
            if root:
                left = dfs(root.left)
                right = dfs(root.right)
                if root.val >= left and root.val >= right:
                    nonlocal count
                    count += 1
                    return root.val
                return max(left, right)
            else:
                return 0

        dfs(root)
        return count

```



Use a postorder dfs to calculate the maximum of every subtree. The answer increases by 1 whenever `node.val == subtree_max`.
{% endtab %}
{% endtabs %}

