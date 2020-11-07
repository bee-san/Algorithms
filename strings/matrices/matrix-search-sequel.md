# Matrix Search Sequel

{% hint style="info" %}
[https://leetcode.com/problems/search-a-2d-matrix-ii/submissions/](https://leetcode.com/problems/search-a-2d-matrix-ii/submissions/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Example:**

Consider the following matrix:

```text
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = `5`, return `true`.

Given target = `20`, return `false`.
{% endtab %}

{% tab title="Answer" %}
First, lets try a bruteforce solution. 

```python
def solutiion(matrix, target):
    for i in matrix:
        for y in i:
            if y == target:
                return True
    return False
```

And then we notice something. The last item in each row is always the largest.

If our target value is more than that value, we can just skip searching that row.

```python
def solution(matrix, target):
     for i in range(0, len(matrix)):
            if matrix[i][-1] < target:
                continue
            for y in matrix[i]:
                if y == target:
                    return True
                    
        return False
```

But our searching of each row is inefficient. What if we used binary search?

```python
def solution(matrix, target):
    for i in range(0, len(matrix)):
        if matrix[i][-1] < target:
            continue
    
        left, right = 0, len(matrix[i])
        while left < right:
            mid = (left + right) // 2
            if matrix[i][mid] >= target:
                if matrix[i][mid] == target:
                    return True
                left = mid + 1
            else:
                right = mid
        
                
    return False
```

I was doing a mock interview and this is where the time ran out. After this, I switched to Leetcode so these solutions may not work on Leetcode. But also:

![](../../.gitbook/assets/image%20%2822%29.png)

Strange that my solution was 100% speed when it's not efficient. Anyway, here's the most optimal solution:

We noticed that the last item in the column is the largest in that row. 

But columns are sorted too.

```text
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
```

Look at the first column. It reads:

```text
1
2
3
10
18
```

We can remove or ignore columns that do not fit in 

We can perform binary search from the bottom left taking this into account.  
We start search the matrix from top right corner, initialize the current position to top right corner, if the target is greater than the value in current position, then the target can not be in entire row of current position because the row is sorted.

if the target is less than the value in current position, then the target can not in the entire column because the column is sorted too. We can rule out one row or one column each time, so the time complexity is O\(m+n\).

```python
class Solution:
    def searchMatrix(self, matrix, target):
                
        i, j = len(matrix) - 1, 0
        while(i >= 0 and i < len(matrix) and j >=0 and j < len(matrix[0])):
            if(matrix[i][j] == target): 
                # target is found
                return True
            if(matrix[i][j] > target):  
                # Not this column
                i -= 1
            if(matrix[i][j] < target):  
                # Not this rpw
                j += 1              
        return False
```

{% embed url="https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/" %}
{% endtab %}
{% endtabs %}

