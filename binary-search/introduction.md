# Introduction

Based on this:

{% embed url="https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/discuss/777019/Python-Clear-explanation-Powerful-Ultimate-Binary-Search-Template.-Solved-many-problems." %}

Binary Search is an algorithm for searching for data in sorted data.

We split the search space into two halves and only keep the half that probably has the search target and throw away the other half that cannot contain the target.

In this way, we reduce the search sapce to half at every step until we find the target.

Binary search helps us reduce our O\(n\) linear search algorithm into O\(log n\).

We often want to implement a slightly modified binary search. Here are some typical problems we may face:

* When do we exit the loop? Should we use left &lt; right or &lt;= right?
* How to initialise the boundary variable left and right
* How to update the boundary? How to choose the appropriate combination from `left = mid, left = mid + 1` and `right = mid, right = mid - 1`?

A rather common misunderstanding of binary search is that people often think this technique could only be used in simple scenario like "Given a sorted array, find a specific value in it". As a matter of fact, it can be applied to much more complicated situations.




