# Minimum Height Trees

{% hint style="info" %}
[https://leetcode.com/problems/minimum-height-trees/](https://leetcode.com/problems/minimum-height-trees/)
{% endhint %}

{% tabs %}
{% tab title="Problem" %}
A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of `n` nodes labelled from `0` to `n - 1`, and an array of `n - 1` `edges` where `edges[i] = [ai, bi]` indicates that there is an undirected edge between the two nodes `ai` and `bi` in the tree, you can choose any node of the tree as the root. When you select a node `x` as the root, the result tree has height `h`. Among all possible rooted trees, those with minimum height \(i.e. `min(h)`\)  are called **minimum height trees** \(MHTs\).

Return _a list of all **MHTs'** root labels_. You can return the answer in **any order**.

The **height** of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

![](../../.gitbook/assets/image%20%282%29.png)

```text
Input: n = 4, edges = [[1,0],[1,2],[1,3]]
Output: [1]
Explanation: As shown, the height of the tree is 1 when the root is the node with label 1 which is the only MHT.
```
{% endtab %}

{% tab title="Answer" %}
As the hints suggest, this problem is related to the [graph](https://en.wikipedia.org/wiki/Graph_%28abstract_data_type%29) data structure. Moreover, it is closely related to the problems of [Course Schedule](https://leetcode.com/problems/course-schedule/) and [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/). This relationship is not evident, yet it is the key to solve the problem, as one will see later.

First of all, as a _**straight-forward**_ way to solve the problem, we can simply follow the requirements of the problem, as follows:

* Starting from each node in the graph, we treat it as a _**root**_ to build a tree. Furthermore, we would like to know the distance between this root node and the rest of the nodes. The maximum of the distance would be the _**height**_ of this tree.
* Then according to the definition of **Minimum Height Tree** \(MHT\), we simply filter out the roots that have the minimal height among all the trees.

The first step we describe above is actually the problem of [Maximum Depth of N-ary Tree](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/), which is to find the maximum distance from the root to the leaves nodes. For this, we can either apply the [Depth-First Search](https://leetcode.com/explore/learn/card/queue-stack/232/practical-application-stack/) \(**DFS**\) or [Breadth-First Search](https://leetcode.com/explore/learn/card/queue-stack/231/practical-application-queue/) \(**BFS**\) algorithms.

Without a rigid proof, we can see that the above straight-forward solution is _correct_, and it would work for most of the test cases.

However, this solution is not efficient, whose time complexity would be \mathcal{O}\(N^2\)O\(N2\) where NN is the number of nodes in the tree. As one can imagine, it will result in _**Time Limit Exceeded**_ exception in the online judge.

As a spoiler alert, in this article, we will present a [_**topological sorting**_](https://en.wikipedia.org/wiki/Topological_sorting) alike algorithm with time complexity of O\(n\), which is also the algorithm to solve the well-known course schedule problems.

## Approach 1
{% endtab %}
{% endtabs %}



