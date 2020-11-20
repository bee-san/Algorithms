# Merging Binary Trees

{% hint style="info" %}
[https://leetcode.com/problems/merge-two-binary-trees](https://leetcode.com/problems/merge-two-binary-trees)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given two binary trees `node0` and `node1`, return a merge of the two trees where each value is equal to the sum of the values of the corresponding nodes of the input trees. If only one input tree has a node in a given position, the corresponding node in the new tree should match that input node.

For example, given

```text
   0         7
  / \       / \
 3   2     5   1
    /
   3
```

Return

```text
   7
  / \ 
 8   3
    /
   3
```

**Constraints**

* `n ≤ 100,000` where `n` is the number of nodes in `node0`
* `m ≤ 100,000` where `m` is the number of nodes in `node1`

#### Example 1

**Input**

```text
node0 = [1, [0, null, null], null]
node1 = [1, null, null]
```

**Output**

```text
[2, [0, null, null], null]
```
{% endtab %}

{% tab title="Answer" %}
We are performing an in-order traversal \(note that pre-order and post-order work as well\).

We perform this on both trees at the same time, and add the nodes at each level.

By performing it at the same same, we are traversing the trees in the exact same way which means all we need to do is add the values of the nodes.Implementation

Our basecases are when either of the nodes are none. If they are, we return the other node.

This fixes the problem of our tree looking like:

```text
                  10
                  +
                  |
                  |
                  |
                  |
                  |
                  |
                  |
                  |
                  |
       +----------+------------+
       |                       |
       |                       |
       |                       +
      9|                       7
+----------+
|          |
+         ++
12         11

```

\(Not a binary tree, but it still explains the problem\).

When we reach 7 on the other side, if we didn't return the left nodes we would exit the program.

This way essentially we are saying "add X and Y together, but if X doesn't exist then 0 + Y = Y, so return Y. Same for if Y doesn't exist, return X".

We need to use a traversal method, any of them work for this problem.

## Key Takeaways

* Traverse both trees at same time
* Compare node1 and node1 from tree1 and tree2
* Merge it all into one tree in-place
* Return the tree. Note: recursion goes from bottom-up, so when we return node0 we return the whole tree.

Time Complexity

O\(h + h1\) where H is the height of tree 0 and H1 is the height of tree 1.Space Complexity

O\(1\) space since we do it entirely in-place, no extra data structure is needed.

```python
# class Tree:
#     def __init__(self, val, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def solve(self, node0, node1):
        if not node0:
            return node1
        if not node1:
            return node0

        node0.left = self.solve(node0.left, node1.left)
        node0.val += node1.val
        node0.right = self.solve(node0.right, node1.right)

        return node0
```
{% endtab %}
{% endtabs %}

