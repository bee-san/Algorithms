# Matrix Search Sequel

```python
class Solution:
    def solve(self, matrix, target):
        # Linear Search
        """
        nums = []
        for i in matrix:
            for y in i:
                if y == target:
                    return True
        return False
        
        O(n+m)
        """
        """
        # ending < target
        for i in range(0, len(matrix)):
            if matrix[i][-1] < target:
                continue
            for y in matrix[i]:
                if y == target:
                    return True
                    
        return False
        # O(n + m)
        """
        # ending < target
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
            
                    
        return left == target
```

[https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/](https://www.geeksforgeeks.org/search-in-row-wise-and-column-wise-sorted-matrix/)

