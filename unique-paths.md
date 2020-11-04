# Unique Paths

{% hint style="info" %}
[https://leetcode.com/problems/unique-paths/](https://leetcode.com/problems/unique-paths/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
A robot is located at the top-left corner of a `m x n` grid \(marked 'Start' in the diagram below\).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid \(marked 'Finish' in the diagram below\).

How many possible unique paths are there?

![](.gitbook/assets/image%20%281%29.png)



```text
Input: m = 3, n = 7
Output: 28
```

## Example 2

```text
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
```
{% endtab %}

{% tab title="Answer" %}
Our base case is:

* The top left hand corner \[0\]\[0\] = 1

There is 1 unique path to that square \(it starts on it\)

Then we need to work out the subproblems.

We will assume the subproblem is to work out all total paths to \[0\]\[1\], \[1\]\[1\], \[0\]\[1\] and so on.

In total, for each grid on the square we want to work out all possible paths to that grid.

We are only allowed to move right or down at any given point.

This means that we need to calculate total path for the top row and the left column, as we cannot travel left / down **to** them.

For every other grid, the value of that grid is the value from the grid to its left and the grid above it.

Therefore our algorithm looks like:

* grid\[0\]\[0\] = 1
* Calculate values for grid\[0\]\[n\]
* Calculate values for grid\[n\]\[0\]
* `grid[i][j] = grid[i][j - 1] + grid[i - 1][j]`

Let's visualise this.

![](.gitbook/assets/image%20%283%29.png)

We have a 4x4 grid with coordinates. Let's look at \(1, 1\)

![](.gitbook/assets/image%20%284%29.png)

The sum for \(1, 1\) is the sum for \(1, 0\) added to the sum for \(0, 1\).

To calculate this, we remove 1 from each side.

So the sum is:

$$
new\_coords = [i - 1][j] + [i][j - 1]
$$

## Coding it

Let's start out by generating our DP array.

```python
dp = [[1 for _ in range(n)] for _ in range(m)]
```

Remember how our previous DP problems required us to build the table array first? This is us building an n x m table!  
  
We fill the top row and left row with 1, as we cannot traverse them as we're only allowed to go down or right.  
  
Since we filled the top and left rows, we do not need to include them so we can start at \(1, 1\).

This makes our code look like this:

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[-1][-1]
```
{% endtab %}
{% endtabs %}



