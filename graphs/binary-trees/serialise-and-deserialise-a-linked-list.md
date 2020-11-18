# Serialise and Deserialise a Linked List

{% hint style="info" %}
[https://leetcode.com/problems/serialize-and-deserialize-bst/](https://leetcode.com/problems/serialize-and-deserialize-bst/)
{% endhint %}

{% tabs %}
{% tab title="Question" %}
Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a **binary search tree**. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.

**The encoded string should be as compact as possible.**

**Example 1:**

```text
Input: root = [2,1,3]
Output: [2,1,3]
```

**Example 2:**

```text
Input: root = []
Output: []
```
{% endtab %}

{% tab title="Answer" %}
{% embed url="https://www.youtube.com/watch?v=suj1ro8TIVY" %}

![](../../.gitbook/assets/image%20%2873%29.png)

Preorder works well, as we look for a first value and pass off the rest.

![](../../.gitbook/assets/image%20%2872%29.png)

What does this function take?

The core thing we care about tree problems is a key. We have a tree, what is the focus of our tree? A single node!

We want to process a single treeNode.

The number 1 thing we're thinking is "how do we process this single node, and defer all the otherwork and let the recursion do its job?"

If node is null, we cannot serailise it.

![](../../.gitbook/assets/image%20%2881%29.png)

We return something for Null nodes.

But, if the node has a value then we want to return that value append to the serialisation of the left subtree and the right subtree.

But, how did we even get those 2 serialisations? We need to find them.

We defer the work. 

![](../../.gitbook/assets/image%20%2874%29.png)

I know the answer to my subtree, but first serialise left and serialise right. Then when you get back to me we just append the value to the serialisation.

But you may see a problem.

![](../../.gitbook/assets/image%20%2879%29.png)

Where do the numbers begin and where do the numbers end?

We need some way to separate these numbers. We can use a delimiter such as a comma.

![](../../.gitbook/assets/image%20%2877%29.png)

If we run it again we get:

![](../../.gitbook/assets/image%20%2876%29.png)

We have no serialised this tree.

Now we can deserlise.

## Deserialise

We need to make meaning of our data.

First, we need to start with what our representation looks like.

![](../../.gitbook/assets/image%20%2875%29.png)

For each value, we either wanna generate a node or return null.

Let's make a helper.

![](../../.gitbook/assets/image%20%2878%29.png)

![](../../.gitbook/assets/image%20%2871%29.png)

We need to grab the item at index 0. Can we just grab the first actual value in the string? When we pass it in, we didn't split it at the commas. Let's do that.

![](../../.gitbook/assets/image%20%2869%29.png)

Do we even need to pass around state? The problem doesn't allow us to do.

Let's delete everything.  
One structure we can use is a queue.

The reason we think of a queue is a line. One by one, the first node to be deserialised is the leading item. And then the next one, and the next one and so on.

It makes sense to have a line, waiting in line -- a queue.

![](../../.gitbook/assets/image%20%2883%29.png)

Now:

![](../../.gitbook/assets/image%20%2885%29.png)

If a node is null, return null.

![](../../.gitbook/assets/image%20%2884%29.png)

The value has to be an integer, so we can pull it out into some temp variable.

Deserialise what is on the left, and then on the right.

![](../../.gitbook/assets/image%20%2882%29.png)

What we want to do is run it left and right, but what do we set it equal to?

We want to set the subtrees. What we need to do is set nodes left, and nodes right.

![](../../.gitbook/assets/image%20%2870%29.png)

All we need to worry about is myself, a single node. Then we defer everything to the recursion.

Then we need to return myself as I populated myself.

![](../../.gitbook/assets/image%20%2880%29.png)

```python
from collections import deque
class Codec:

    def serialize(self, root: TreeNode) -> str:
        """Encodes a tree to a single string.
        """
        
        # record of preorder traversal path
        path_of_preorder = []
        
        # Generate pre-order traversal path of binary search tree
        def helper( node ):
            
            if node:
                path_of_preorder.append( node.val )
                helper( node.left )
                helper( node.right )
        
        # ---------------------------------------------
        helper( root )
        # output as string, each node is separated by '#'
        return '#'.join( map(str, path_of_preorder) )
                
        
        

    def deserialize(self, data: str) -> TreeNode:
        """Decodes your encoded data to tree.
        """
        if not data:
            # corner case handle for empty tree
            return None
        
        # convert input string into doubly linked list of integer type, each node is separated by '#'
        node_values = deque(  int(value) for value in data.split('#') )
        
        # Reconstruct binary search tree by pre-order traversal
        def helper( lower_bound, upper_bound):
            
            if node_values and lower_bound < node_values[0] < upper_bound:
                
                root_value = node_values.popleft()
                root_node = TreeNode( root_value )
                
                root_node.left = helper( lower_bound, root_value )
                root_node.right = helper( root_value, upper_bound )
                
                return root_node
        
        # ---------------------------------------------
        
        return helper( float('-inf'), float('inf')) 
```
{% endtab %}
{% endtabs %}

