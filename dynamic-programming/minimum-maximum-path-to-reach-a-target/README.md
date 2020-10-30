# Minimum \(Maximum\) Path to Reach a Target

Given a target find minimum \(maximum\) cost / path / sum to reach the target.

 We can do this by choosing the minimum \(maximum\) path among all possible paths before the current state, and then add the value for the current state.

```text
routes[i] = min(routes[i-1], routes[i-2], ... , routes[i-k]) + cost[i]
```

An example is:

```python
for i in range(2, len(cost)):
    cost[i] = min(cost[i] + cost[i - 1], cost[i] + cost[i - 2])
return min(cost[-1], cost[-2])
```



