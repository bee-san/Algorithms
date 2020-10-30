# Unique Elements

## BitMaps

Bitmaps are arrays of specific sizes where every element is either True or False. They can be used for many things but are an extremely efficient method of storage for certain algorithms.

One example is the act of whether something is open or closed, in or not in a set. Anything that is quantifiable as a True / False operation.

An example of a Bitmap is:

```python
[False, False, False, False, True]
```

Let's say you portscan a website to see what ports are open with [RustScan](http://github.com/rustScan/RustScan). The position in the array relates to the port number. So we have port numbers 1 through 5. We start with all ports closed \(False\), but our scanner reports that port 5 is open so we set it to True.

We use the size of the array, the indices, and True / False values to map True / False values to a domain.

{% tabs %}
{% tab title="Question" %}
Implement an algorithm to determine if a string has all unique characters 
{% endtab %}

{% tab title="Answer" %}
```python
def is_unique(text):

    # BitMap of chars
    char_set = [False for _ in range(128)]
    for char in text:
        val = ord(char)
        if char_set[val]:
            # Char already in string
            # so it's not unique
            return False
        char_set[val] = True

    return True
```

Assuming the input is Ascii only \(ask your interviewer\) we create a bitmap of \[False\] \* 128 \(128 is the length of Ascii\).

We then go through the text one char at a time, and for every char we set it to True.

If we see a char that is already set to True, we return False as that char has appeared twice.

This algorithm is O\(n\) time and O\(n\) space complexity.
{% endtab %}
{% endtabs %}

