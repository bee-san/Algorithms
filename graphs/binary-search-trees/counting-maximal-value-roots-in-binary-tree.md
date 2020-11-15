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

We use a post order DFS here. Post order means:

* Left children
* Visits right children
* Visit current node

We use post-order traversal to visit subtrees recursively. By visiting each subtree, we solve the problem at that subtree and eventually solve the full problem.

We need to do this because of this part of the question:

> all of its descendants.

Our algorithm will go down to these subtrees first:

![](../../.gitbook/assets/image%20%2854%29.png)

And then these:

![](../../.gitbook/assets/image%20%2849%29.png)

And finally this:

![](../../.gitbook/assets/image%20%2850%29.png)

The answer increments by 1 whenever `node.val == subtree_max`.
{% endtab %}
{% endtabs %}

## TODO write preorder s postorder vs in order

