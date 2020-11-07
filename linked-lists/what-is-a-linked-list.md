# What is a Linked List?

Linked lists are a data structure. They consist of nodes which hold 2 values:

* Data - The data that node stores
* Next - The node next in the list

![](../.gitbook/assets/image%20%2820%29.png)

You can also have doubly linked lists, which remembers its previous node.

![](../.gitbook/assets/image%20%2819%29.png)

## Advantages & Disadvantages

**Linked lists are preferable over arrays when:**

1. you need constant-time insertions/deletions from the list \(such as in real-time computing where time predictability is absolutely critical\)
2. you don't know how many items will be in the list. With arrays, you may need to re-declare and copy memory if the array grows too big
3. you don't need random access to any elements
4. you want to be able to insert items in the middle of the list \(such as a priority queue\)

**Arrays are preferable when:**

1. you need indexed/random access to elements
2. you know the number of elements in the array ahead of time so that you can allocate the correct amount of memory for the array
3. you need speed when iterating through all the elements in sequence. You can use pointer math on the array to access each element, whereas you need to lookup the node based on the pointer for each element in linked list, which may result in page faults which may result in performance hits.
4. memory is a concern. Filled arrays take up less memory than linked lists. Each element in the array is just the data. Each linked list node requires the data as well as one \(or more\) pointers to the other elements in the linked list.

Array Lists \(like those in .Net\) give you the benefits of arrays, but dynamically allocate resources for you so that you don't need to worry too much about list size and you can delete items at any index without any effort or re-shuffling elements around. Performance-wise, arraylists are slower than raw arrays.

{% embed url="https://www.youtube.com/watch?v=\_jQhALI4ujg" %}



