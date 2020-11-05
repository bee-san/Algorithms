# Minimum Cost Tree From Leaf Values

{% hint style="info" %}
[https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given an array `arr` of positive integers, consider all binary trees such that:

* Each node has either 0 or 2 children;
* The values of `arr` correspond to the values of each **leaf** in an in-order traversal of the tree.  _\(Recall that a node is a leaf if and only if it has 0 children.\)_
* The value of each non-leaf node is equal to the product of the largest leaf value in its left and right subtree respectively.

Among all possible binary trees considered, return the smallest possible sum of the values of each non-leaf node.  It is guaranteed this sum fits into a 32-bit integer.

```text
Input: arr = [6,2,4]
Output: 32
Explanation:
There are two possible trees.  The first has non-leaf node sum 36, and the second has non-leaf node sum 32.

    24            24
   /  \          /  \
  12   4        6    8
 /  \               / \
6    2             2   4
```
{% endtab %}

{% tab title="Answer" %}
[https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/339959/One-Pass-O\(N\)-Time-and-Space](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/339959/One-Pass-O%28N%29-Time-and-Space)  
**DP Solution**

Find the cost for the interval `[i,j]`.  
To build up the interval `[i,j]`,  
we need to split it into left subtree and sub tree,  
`dp[i, j] = dp[i, k] + dp[k + 1, j] + max(A[i, k]) * max(A[k + 1, j])`

We are given a list of all the leaf nodes values for certain binary trees, but we do not know which leaf nodes belong to left subtree and which leaf nodes belong to right subtree. 

Since the given leaf nodes are result of inorder traversal, we know there will be pivots that divide arr into left and right, nodes in the left build left subtree and nodes in the right build right subtree. 

For each subtree, if we know the minimum sum, we can use it to build the result of the parent tree, so the problem can be divided into subproblems, and we have the following general transition equation \(res\(i, j\) means the minimum non-leaf nodes sum with leaf nodes from arr\[i\] to arr\[j\]\):

```python
class Solution:
    def mctFromLeafValues(self, arr: List[int]) -> int:
        return self.helper(arr, 0, len(arr) - 1, {})
        
    def helper(self, arr, l, r, cache):
        if (l, r) in cache:
            return cache[(l, r)]
        if l >= r:
            return 0
        
        res = float('inf')
        for i in range(l, r):
            rootVal = max(arr[l:i+1]) * max(arr[i+1:r+1])
            res = min(res, rootVal + self.helper(arr, l, i, cache) + self.helper(arr, i + 1, r, cache))
        
        cache[(l, r)] = res
        return res
```

### Bottom Up

```python
class Solution:
    def mctFromLeafValues(self, arr: List[int]) -> int:
        n = len(arr)
        dp = [[float('inf') for _ in range(n)] for _ in range(n)]
        for i in range(n):
            dp[i][i] = 0
        
        for l in range(2, n + 1):
            for i in range(n - l + 1):
                j = i + l - 1
                for k in range(i, j):
                    rootVal = max(arr[i:k+1]) * max(arr[k+1:j+1])
                    dp[i][j] = min(dp[i][j], rootVal + dp[i][k] + dp[k + 1][j])
        return dp[0][n - 1]
```

## DP Complexity

Second question after this dp solution,  
**what's the complexity?**  
`N^2` states and `O(N)` to find each.  
So this solution is `O(N^3)` time and `O(N^2)` space.

You thought it's fine.  
After several nested for loop, you got a happy green accepted.  
You smiled and released a sigh as a winner.

What a great practice for DP skill!  
Then you noticed it's medium.  
That's it, just a standard medium problem of dp.  
Nothing can stop you. Even dp problem.  
  


## True story

So you didn't **Read** and **Upvote** this post.  
\(upvote is a good mark of having read\)  
One day, you meet exactly the same solution during an interview.  
Your heart welled over with joy,  
and you bring up your solution with confidence.

One week later, you receive an email.  
The second paragraph starts with a key word "Unfortunately".

**What the heck!?**  
You solved the interview problem perfectly,  
but the company didn't appreciate your talent.  
What's more on earth did they want?  
**WHY?**  
  


## **Why**

Here is the reason.  
This is not a dp problem at all.

Because dp solution test all ways to build up the tree,  
including many unnecessay tries.  
Honestly speaking, it's kinda of brute force.  
Yes, brute force testing, with memorization.  
  


## **Intuition**

Let's review the problem again.

When we build a node in the tree, we compared the two numbers `a` and `b`.  
In this process,  
the smaller one is removed and we won't use it anymore,  
and the bigger one actually stays.

The problem can translated as following:  
Given an array `A`, choose two neighbors in the array `a` and `b`,  
we can remove the smaller one `min(a,b)` and the cost is `a * b`.  
What is the minimum cost to remove the whole array until only one left?

To remove a number `a`, it needs a cost `a * b`, where `b >= a`.  
So `a` has to be removed by a bigger number.  
We want minimize this cost, so we need to minimize `b`.

`b` has two candidates, the first bigger number on the left,  
the first bigger number on the right.

The cost to remove `a` is `a * min(left, right)`.  
  


## **Solution 1**

With the intuition above in mind,  
the explanation is short to go.

We remove the element form the smallest to bigger.  
We check the `min(left, right)`,  
For each element `a`, `cost = min(left, right) * a`

Time `O(N^2)`  
Space `O(N)`

```python
def mctFromLeafValues(self, A):
    res = 0
    while len(A) > 1:
        i = A.index(min(A))
        res += min(A[i - 1:i] + A[i + 1:i + 2]) * A.pop(i)
    return reS
```

## **Solution 2: Stack Soluton**

we decompose a hard problem into reasonable easy one:  
Just find the next greater element in the array, on the left and one right.  
Refer to the problem [503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/discuss/98270/JavaC++Python-Loop-Twice)  
  


Time `O(N)` for one pass  
Space `O(N)` for stack in the worst cases

```python
def mctFromLeafValues(self, A):
    res = 0
    stack = [float('inf')]
    for a in A:
        while stack[-1] <= a:
            mid = stack.pop()
            res += mid * min(stack[-1], a)
        stack.append(a)
    while len(stack) > 2:
        res += stack.pop() * stack[-1]
    return res
```
{% endtab %}
{% endtabs %}



