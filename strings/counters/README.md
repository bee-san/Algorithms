# Counters

Here's another common pattern you may see.

```python
counter = 0
for i in n: # n is a list of items
    if condition(i):
        counter += 1
    else:
        counter -= 1
```

We have a single counter and we increment it / decrement it based on a condition. 

We keep a counter and we perform things based on this counter.

Another example is:

```python
counter = 0
while counter < len(s):
    if condition(s[counter]):
        counter += 1
```

