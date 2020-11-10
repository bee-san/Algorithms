# Sliding Window

The sliding window technique eases the task of finding optimal _chunks of contiguous data_ that meet a certain condition:

* Longest subarray that …
* Shortest substring containing …
* Etc

You can think of it as another variation of the two pointer technique, where pointers are updated separately based on a certain condition. Below is the basic recipe for this type of problems, in pseudocode:  


```text
Create two pointers, l, and r
Create variable to keep track of the result (res)

Iterate until condition A is satisfied:
  Based on condition B:
update l, r or both
Update res
Return res
```

