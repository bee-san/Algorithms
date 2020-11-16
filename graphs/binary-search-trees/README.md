# Binary Search Trees

A binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child

## Binary Tree vs Binary Search Tree

A _binary search tree_ is a binary tree in which every node fits a specific ordering property.

All left descendants ≤ n &lt; all right descendants

This must be true for each node, n.

Basically, the entire left side must always be smaller than the right on the same level.

This definition can change slightly. Under some conditions, the tree cannot have duplicate values. Or the duplicate values will be on the right side, or on the left. All are valid, so check with your interviewer.

When given a question, many candidates assume the interviewer means a binary search tree.

Be sure to ask!

**A binary search tree implies that for each node, its left descendants are less than or equal to the current node, which is less then the right descendants.**

## Balanced vs Unbalanced

Ask your interviewer whether the tree is balanced or unbalanced

Note: balancing a tree does not mean left and right subtrees are exactly the same size.

One way of thinking about this is that a balanced tream means "not terribly unbalanced". It's balanced enough to ensure O\(log n\) insert and find, but it's not necessarily as balanced as it could be.

## Complete Binary Tree

Every level of the tree is fully filled, except for perhaps the last level. The last level is filled left to right.

![](../../.gitbook/assets/image%20%2852%29.png)

## Full Binary Trees

Every node has either zero or two children. No nodes have only one child.

![](../../.gitbook/assets/image%20%2853%29.png)

## Perfect Binary Trees

Both full and complete. All leaf nodes will be at the same level, and this level has the maximum number of nodes.

Perfect trees are rare in interviews and in real life. Do not assume a binary tree is perfect in an interview.

![](../../.gitbook/assets/image%20%2851%29.png)



