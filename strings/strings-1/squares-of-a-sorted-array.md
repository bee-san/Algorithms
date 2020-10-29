# Squares of a Sorted Array

{% hint style="info" %}
[https://leetcode.com/explore/learn/card/fun-with-arrays/521/introduction/3240/](https://leetcode.com/explore/learn/card/fun-with-arrays/521/introduction/3240/)
{% endhint %}

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

```python
   def sortedSquares(self, A: List[int]) -> List[int]:
        for i in range(len(A)):
            A[i] *= A[i]
        A.sort()
        return A
```
{% endtab %}
{% endtabs %}

