# Pigeonhole

{% tabs %}
{% tab title="First Tab" %}
You are given a list `nums` of length `n + 1` picked from the range `1, 2, ..., n`. By the [pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle), there must be a duplicate. Find and return it. There is guaranteed to be exactly one duplicate.

Bonus: Can you do this in linear time and constant space?
{% endtab %}

{% tab title="Second Tab" %}
This solution uses the formula for the sum of numbers from 1 to n. Then the duplicate number is the number left over subtracting that sum, which we will call the expected sum, from the actual sum of all numbers in the list.

From [here](https://binarysearch.com/room/The-Palindome-4G4AiUpuLO/editorials/1520494?questionsetIndex=1).

```python
class Solution:
    def solve(self, nums):
        n = len(nums) - 1
        return sum(nums) - n * (n + 1) // 2
```
{% endtab %}
{% endtabs %}

