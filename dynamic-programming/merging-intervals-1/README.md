# Merging Intervals

Given a set of numbers find an optimal solution for a problem considering the current number and the best you can get from the left and right sides.

We can approach this by finding all optimal solutions for every interval and return the best possible answer.

```text
// from i to j
dp[i][j] = dp[i][k] + result[k] + dp[k+1][j]
```

Get the best from the left and right sides and add a solution for the current position.

```java
for(int l = 1; l<n; l++) {
   for(int i = 0; i<n-l; i++) {
       int j = i+l;
       for(int k = i; k<j; k++) {
           dp[i][j] = max(dp[i][j], dp[i][k] + result[k] + dp[k+1][j]);
       }
   }
}
 
return dp[0][n-1]
```

