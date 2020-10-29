# Find Numbers with Even Number of Digits

{% hint style="info" %}
[https://leetcode.com/problems/find-numbers-with-even-number-of-digits/](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
 Given an array `nums` of integers, return how many of them contain an **even number** of digits.

```text
Input: nums = [12,345,2,6,7896]
Output: 2
Explanation: 
12 contains 2 digits (even number of digits). 
345 contains 3 digits (odd number of digits). 
2 contains 1 digit (odd number of digits). 
6 contains 1 digit (odd number of digits). 
7896 contains 4 digits (even number of digits). 
Therefore only 12 and 7896 contain an even number of digits.
```
{% endtab %}

{% tab title="Answer" %}
This answer requires knowledge of somethings.

### Modulus

To find out whether a number is even or not, we use the modulus operator. Y % X implies that Y is divided by X, and whatever the remainder is will be the result.

If we divide a number by 2, and it's odd we will have a remainder.

`6 % 2 == 0 # False`

The number being divided is called the **dividend**, and the number that divides the dividend is called the **divisor**.

We can also use modulus for other things, such as checking if a number is odd. Or turning a list into a loop. If we have a list that is size 6, and we want to iterate 9 numbers but have it loop back around, we can use modulus for this.

6 % 9 = 3, which means our index will be at 3.

## Solution

For every number in nums, we check to see if its digits are even. If it is, we generate a tuple of these numbers \(this is similar to list generation. We could have used `[function for  i in list]`. See my [Python book](https://github.com/bee-san/Python-Zero-to-Hero) for more info.

We do this by calculating the length of the string of the number. This turns the number into an array \(string\), which as a length. The number 6 as a string will be length 1. The number 12 as a string will be length 2.

For every number, 

* Turn it into a string
* Calculate its length
* Calculate whether it is even
* If it is, store `True` in the tuple.
* Sum all the `Trues` in the tuple to work out how many numbers match this property.



```python
def findNumbers(self, nums: List[int]) -> int:
    return sum(len(str(n)) % 2 == 0 for n in nums) 
```

This code is O\(n\) time complexity, as it touches every list item exactly once.

The space complexity is O\(n\), but note that because we are creating a tuple / generator of True values our space complexity will be slightly higher than n, but under Big O notational rules it is still O\(n\).
{% endtab %}
{% endtabs %}

