# Maximum Difference Between Node and Ancestor

{% hint style="info" %}
[https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the `root` of a binary tree, find the maximum value `V` for which there exist **different** nodes `A` and `B` where `V = |A.val - B.val|` and `A` is an ancestor of `B`.

A node `A` is an ancestor of `B` if either: any child of `A` is equal to `B`, or any child of `A` is an ancestor of `B`.

![](../../.gitbook/assets/image%20%2826%29.png)



```text
Input: root = [8,3,10,1,6,null,14,null,null,4,7,13]
Output: 7
Explanation: We have various ancestor-node differences, some of which are given below :
|8 - 3| = 5
|3 - 7| = 4
|8 - 1| = 7
|10 - 13| = 3
Among all possible differences, the maximum value of 7 is obtained by |8 - 1| = 7.
```
{% endtab %}

{% tab title="Answer" %}
The simplest solution is to bruteforce every node and calculate the sum. This takes O\(n^2\) time. But, can we do better?

Since the problem asks us the Maximum Difference, maybe we do not need to compare all ancestor for a given node and we only need to compare the ancestors with Maximum value and Minimum value.

Therefore, for a given node, we only need the maximum value and the minimum value from the root to this node.

To achieve this, we can define a function `helper` to start recursion, which receives a node and two integers, the maximum and minimum value of its ancestors, as input.

In the function `helper`, we need to update the maximum difference, the current maximum value, and the current minimum value.

_Step 1:_ Initialize a variable `result` to record the required maximum difference.

_Step 2:_ Define a function `helper`, which takes three arguments as input.

* The first argument is the current node, and the second and third arguments are the maximum and minimum values along the root to the current node, respectively.
* In the function `helper`, update `result` and call `helper` on the left and right subtrees.

_Step 3:_ Run `helper` on the `root`. It will automatically do recursion on every node.

_Step 4:_ Finally, return `result`.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxAncestorDiff(self, root: TreeNode) -> int:
        if not root:
            return 0
        # record the required maximum difference
        self.result = 0

        def helper(node, cur_max, cur_min):
            if not node:
                return
            # update `result`
            self.result = max(self.result, abs(cur_max-node.val),
                              abs(cur_min-node.val))
            # update the max and min
            cur_max = max(cur_max, node.val)
            cur_min = min(cur_min, node.val)
            helper(node.left, cur_max, cur_min)
            helper(node.right, cur_max, cur_min)

        helper(root, root.val, root.val)
        return self.result
```
{% endtab %}
{% endtabs %}



