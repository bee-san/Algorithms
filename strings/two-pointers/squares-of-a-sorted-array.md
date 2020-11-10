# Squares of a Sorted Array

{% hint style="info" %}
[https://leetcode.com/explore/learn/card/fun-with-arrays/521/introduction/3240/](https://leetcode.com/explore/learn/card/fun-with-arrays/521/introduction/3240/)
{% endhint %}

## 2 Pointers

The 2 pointers technique is where we have 2 variables pointing at different parts of the array. An example is:

```python
x = [1, 2, 3, 4, 5]
pointer1 = 0
pointer2 = len(x) - 1
while pointer1 <= pointer2:
    print(pointer1 + pointer2)
    pointer1 += 1
    pointer2 -= 1
```

This code adds the largest element to the smallest element and goes inwards into the code.

Very often we'll want 2, 3, 4 pointers in our array. These pointers do not always have to move at the same speed. Having 2 pointers is often an evolution of using 2 for loops. Look at this problem:

> Given an array of sorted numbers and a target sum, find a pair in the array whose sum is equal to the given target.

Given the array is sorted, our first thought might be 2 nested for loops. This is O\(n^2\). We want O\(n\).

We can achieve this with pointers.

Place 1 pointer at the start, and and another pointer at the end.

```python
x = [1, 2, 3, 4, 5]
pointer1 = 0
pointer2 = len(x) - 1
target = 7
```

Now we calculate the sum of the 2 numbers.

```python
1 + 5 = 6
6 < target (7)
```

We know the value is larger, so we move one to the right.

```python
x = [1, 2, 3, 4, 5]
pointer1 = 2 # value 1
pointer2 = 4 # value 5
sum = 7
sum == target
```

This algorithm is O\(n\).

The pointers pattern is an essential pattern for array manipulation, and we will see it come up a lot. Especially with 2 pointers moving at different speeds.

{% tabs %}
{% tab title="Question" %}
Given an array of integers `A` sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.  


```text
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```
{% endtab %}

{% tab title="Answer" %}
There are multiple solutions to this!

## Solution 1 - Python with in-built Sort

```python
   def sortedSquares(self, A: List[int]) -> List[int]:
        for i in range(len(A)):
            A[i] *= A[i]
        A.sort()
        return A
```

This uses built in sort. It should be O\(n log n\) but due to how Python's sorting algorithm works, it's O\(n\) amortised. You can learn about why it's O\(n\) [here](https://skerritt.blog/timsort-the-fastest-sorting-algorithm-youve-never-heard-of/).

Space complexity is O\(1\) as it is entirely in-place. `.sort()` is in place. Ask your interviewer what to do here.

## Solution 2 - Java with Pointers

We can do this in Java using 2 pointers, which is the way the solution was supposed to be written \(it just happens our code is just as fast\):

```java
class Solution {
    public int[] sortedSquares(int[] A) {
        int n = A.length;
        int[] result = new int[n];
        int i = 0, j = n - 1;
        for (int p = n - 1; p >= 0; p--) {
            if (Math.abs(A[i]) > Math.abs(A[j])) {
                result[p] = A[i] * A[i];
                i++;
            } else {
                result[p] = A[j] * A[j];
                j--;
            }
        }
        return result;
    }
}
```

This code is from [here](https://leetcode.com/problems/squares-of-a-sorted-array/discuss/221922/Java-two-pointers-O%28N%29).

## Solution 3 - Python with Pointers

```python
def sortedSquares(self, A):
    answer = collections.deque()
    l, r = 0, len(A) - 1
    while l <= r:
        left, right = abs(A[l]), abs(A[r])
        if left > right:
            answer.appendleft(left * left)
            l += 1
        else:
            answer.appendleft(right * right)
            r -= 1
    return list(answer)
```

From [here](https://leetcode.com/problems/squares-of-a-sorted-array/discuss/222079/Python-O%28N%29-10-lines-two-solutions-explained-beats-100). 

Author explains:

> The question boils down to understanding that if we look at the magnitude of the elements in the array, `A`, both ends "slide down" and converge towards the center of the array. With that understanding, we can use two pointers, one at each end, to iteratively collect the larger square to a list. However, collecting the larger square in a list with `list`'s `append`, results in elements sorted in descending order. To circumvent this, we need to append to the left of the list. Using a `collections.deque()` allows us to append elements to the left of `answer` in O\(1\) time, maintaining the required increasing order.
{% endtab %}
{% endtabs %}



