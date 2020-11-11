# Valid Square

{% hint style="info" %}
[https://leetcode.com/problems/valid-square/](https://leetcode.com/problems/valid-square/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Given the coordinates of four points in 2D space, return whether the four points could construct a square. 

The coordinate \(x,y\) of a point is represented by an integer array with two integers.

**Example:**

```text
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
Output: True
```
{% endtab %}

{% tab title="Answer" %}
Let's draw out our square.

![](../../.gitbook/assets/image%20%2830%29.png)

There are 2 things to note here:

* These numbers do not have to be 0 or 1. They can be 500, 0 etc.

1. A valid square has four equal sides with positive length and four equal angles \(90-degree angles\).

One way to do this is to calculate the number of unique distances. Let's visualise this.

 

![](../../.gitbook/assets/image%20%2827%29.png)

The distance here is 1.

![](../../.gitbook/assets/image%20%2828%29.png)

And here.  
  
This means for all 4 points, we have 1 unique distance \(1 to each point\) in this square.

But, if we include diagonals

![](../../.gitbook/assets/image%20%2829%29.png)

We now have 2.

Using Pythagoras' Therom we can calculate the distance.

We then need to:

* Number of unique distances = 2
* We have 4 distances in total for our square
* We have 2 distances for our diagonals

```python
class Solution(object):
    def validSquare(self, p1, p2, p3, p4):
        points = [p1, p2, p3, p4]
        
        dists = collections.Counter()
        for i in range(len(points)):
            for j in range(i+1, len(points)):
                dists[self.getDistance(points[i], points[j])] += 1
        
        return len(dists.values())==2 and 4 in dists.values() and 2 in dists.values()
        
    def getDistance(self, p1, p2):
        return (p1[0] - p2[0])**2 + (p1[1] - p2[1])**2
```
{% endtab %}
{% endtabs %}







