# Tortoise & Hare Algorithm

The Tortoise and the Hare algorithm implies we have 2 pointers which have these properties:

* Pointer1 is faster than pointer2 \(the hare\)
* Pointer2 is slower than pointer1 \(the tortoise\)

This algorithm can be implemented as a linked list like so:

```java
class Solution {
public:
    ListNode* middleNode(ListNode* head) {

        ListNode* fast = head;
        ListNode* slow = fast;

        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        return slow;        
    }
};
```

Or as a regular list like so:

```python
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

pointer1 = 1
pointer2 = 1

while pointer1 < len(x):
    if pointer2 * 2 == pointer1:
        # update the position of pointer2 to pointer1
        pointer2 = pointer1
```

Although this doesn't hit all nodes in the list, it can be useful to have a pointer trailing behind our hare pointer.



