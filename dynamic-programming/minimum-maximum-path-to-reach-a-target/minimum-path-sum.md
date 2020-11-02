# Minimum Path Sum

{% hint style="info" %}
[https://leetcode.com/problems/minimum-path-sum/](https://leetcode.com/problems/minimum-path-sum/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given a _m_ x _n_ grid filled with non-negative numbers, find a path from top left to bottom right which _minimizes_ the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

```text
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```
{% endtab %}

{% tab title="Hint" %}
2-dimensional dynamic programming array.
{% endtab %}

{% tab title="Answer" %}
```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        if not grid or len(grid) == 0:
            return 0
        
        # get dimensions
        n = len(grid) # no of cells in each col
        m = len(grid[0]) # no of cells in each row
        
        # populate first row using m for no of cells in row
        for i in range(1,m):
            grid[0][i] = grid[0][i] + grid[0][i-1]
        
        # populate first col using n for no of cells in col
        for j in range(1,n):
            grid[j][0] = grid[j-1][0] + grid[j][0]
        
        # populate the rest
        for i in range(1,n):
            for j in range(1,m):
				# get min seen so far plus curr cell value
                grid[i][j] = min(grid[i-1][j],grid[i][j-1]) + grid[i][j]
        
        # return last cell
        return grid[-1][-1]
```

\*\*\*\*[**https://leetcode.com/problems/minimum-path-sum/discuss/554297/Python-In-Place-DP-with-Explanatory-Comments-92ms-\(or-faster-than-97\)**](https://leetcode.com/problems/minimum-path-sum/discuss/554297/Python-In-Place-DP-with-Explanatory-Comments-92ms-%28or-faster-than-97%29)  
****We can tell this is a DP problem because it says "minimise" which is optimising or finding the best possible thing.

We're going to take the big problem we have of going from the top left hand corner to the bottom right hand corner and break that into smaller subproblems.

Let's try going from the top left hand corner to the top right hand corner. If we can calculate the smallest sum to get to any sum on our grid, we can do it to the bottom right hand corner.

Mirror our grid and store the smallest sum to get to that specific square. 

We start off with error checking:

```python
        if not grid or len(grid) == 0:
            return 0
```



{% embed url="https://www.youtube.com/watch?v=ItjZdu6jEMs" %}
{% endtab %}
{% endtabs %}



