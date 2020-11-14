# Count BST nodes in a range

{% hint style="info" %}
[https://binarysearch.com/problems/Count-BST-nodes-in-a-range](https://binarysearch.com/problems/Count-BST-nodes-in-a-range)
{% endhint %}

{% tabs %}
{% tab title="First Tab" %}
Given a binary search tree `root`, and integers `lo` and `hi`, return the count of all nodes in `root` whose values are between `lo` and `hi` \(inclusive\).

For example, with this tree and `lo = 5` and `hi = 10`, return 3 since only `7, 8, 9` are between `[5, 10]`.

```text
   3
  / \
 2   9
    / \
   7   12
  / \
 4   8
```

#### Example 1

**Input**

```text
root = [3, null, [5, null, null]]
lo = 4
hi = 7
```

**Output**

```text
1
```
{% endtab %}

{% tab title="Second Tab" %}
 Intuition

If the current node is larger than the higher bound of the interval, every value in the interval will be to the left of the current node because they are smaller.

If the current node is smaller than the lower bound of the interval, every value in the interval will be to the right of the current node because they are larger.

Otherwise, the current value is in the interval and values can be on both sides of the current node.

```text
# class Tree:
#     def __init__(self, val, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def solve(self, root, lo, hi):
        if not root:
            return 0
        if hi < root.val:
            return self.solve(root.left, lo, hi)
        elif lo > root.val:
            return self.solve(root.right, lo, hi)
        else:
            return self.solve(root.left, lo, hi) + self.solve(root.right, lo, hi) + 1
```
{% endtab %}
{% endtabs %}

