# Distinct Ways

Given a target find a number of distinct ways to reach the target.

$$
routes[i] = routes[i-1] + routes[i-2], ... , + routes[i-k]
$$



```python
d = [float("inf") for i in range(n)]
d[0] = 1
d[1] = 2
for i in range(2, n):
    d[i] = d[i - 1] + d[i - 2]
return d[-1]
```




