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
 Our base case is if the node value is 0, we want to return nothing.

Binary Search Trees have 2 properties that interest us:

* The left node is smaller than the parent
* The right node is larger than or equal to the parent

Therefore if our `hi` is less than the value, we go to the left. This is because:

![](../../.gitbook/assets/image%20%2846%29.png)

lo = 5, hi = 10.

If our hi is less than our value, we want to go to the left. This is because all numbers in the right nodes path will always be larger than hi due to the nature of binary search trees.

If our lo is higher than our value, we want to go to the right. Again, this is because all values in the left hand side are less than our lowest value and due to the nature of binary search trees we want to go to the right.

Eventually, we only go down the paths that have nodes that can possibly be within the appropriate range.

**Left is always smaller than current value, right is always equal to or higher than current value**.

Otherwise, the current value is within the range and we we add together our 2 recursive calls along with adding + 1 to the counter.

```python
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

