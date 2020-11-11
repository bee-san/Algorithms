# Introduction



{% embed url="https://www.youtube.com/watch?v=qq64FrA2UXQ" %}



## What is a number base?

![](../.gitbook/assets/image%20%2836%29.png)

Everyone in base2 is a power of 2.

## Converting from Int to Binary

### First Method

![](../.gitbook/assets/image%20%2835%29.png)

### Second Method

This is my personal favourite method, but to do this you need to know your powers of 2.

Powers of 2 are very important in computer science. Binary is represented as 2 numbers, so if you have 3 circuits then you will have 2³ numbers, 0 through to 7.

The powers of 2 are:

2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192.

And to make an odd number, we add 1 to the list so the list of numbers we need to know becomes: 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, 4096, 8192.

Okay, say we want to represent 15 as a binary number. First we need to split up 15 so it can be made up of powers of 2 + the number 1. The nearest power of 2 that is less than 15 is 8, so we’ll use that. 8 + 4 is 12. 8 + 4 + 2 is 14, so we’re very nearly there! Now we just add a 1. 15 represented as powers of 2 is 8 + 4 + 2 + 1.

Now we know this, we can convert this simply.

The binary to powers of 2 graph looks like this.

![](../.gitbook/assets/image%20%2831%29.png)

If the number uses an 8, put a 1 in the binary box under it to represent that it uses an 8. I much prefer to use this method though:

![](../.gitbook/assets/image%20%2833%29.png)

And then normally we would need to reverse the binary numbers, but in this case because it’s all just 1’s we don’t need to reverse. If we don’t reverse them, we get the wrong binary number as binary is read with the highest order of magnitude to the left, not the lowest. Much like how in “10”, the 1 is a whole place higher than the 0; the same applies for binary.

You can convert binary to decimal in the opposite method.

## Binary Addition

Let’s first review addition in decimal.

```text
23 + 11
```

We first add 3 + 1, that equals 4. then we add 2 + 1, which is 3. So the answer is 34. We add from the right to the left.

Binary addition works the same.

We will begin with one bit \(binary digit\) addition.

```text
0 + 0 = 1
```

and

```text
0 + 1 = 1
```

and

```text
1 + 1 = 10
```

1 + 1 carries us into the next column.

Try it yourself:

```text
111 + 110 = ???
```

Also, pretty much every operator works in the same way it does with binary as with decimal.

## Negative Numbers in Binary

We can represent a binary number by applying a “sign” to it.

In Binary, numbers can be 4 bit, 8 bit, 16 bit, 32 bit and so on. If we have an 8 bit number, it’ll be 8 digits long.

So let’s say we have the number 1 in 8-bit binary, that’ll be represented as: 00000001 to turn this negative, we add a 1 to the front of it 10000001

Although this sometimes causes a problem. Given the number 0 in 8-bit binary: 00000000 we can make it negative by adding a 1 to the front of it. 10000000 But -0, what is that? It’s nothing. It’s impossible. And that’s where the problem comes from.

### Two's Complement

We can make a binary number negative by applying **two’s complement** to it without the need to sign it.

Two’s complement is a really simple algorithm:

* invert all the digits so 0 becomes 1 and 1 becomes 0
* add a +1 to the number

and this makes it negative!

So given the number 15, which is 1111, in 8-bit binary it’ll be: 00001111 So to make this negative we invert all the digits: 11110000 then we add a 1 to the end 11110001 and now this represents -15! How creative and cool!

### Addition with Negative Numbers

Let’s say we have 2 numbers, -3 and -5. In binary these are: 11, 101 and we want to add them together.

But this time we can ignore any carries that go off the end.

So we use the largest power of 2 that can fit both 5 and 3 into it, which is 8. But this time we make it negative.

![](https://miro.medium.com/max/1013/1*jAOMpGY3sQWCM5E6tjUUKw.png)

Now we simply add them. 1 + 1 is 0 carry 1, the next line is 1 + 1 which is 0 so carry that, the next line is 1 + 1 which is 0 so carry that, the next line is 1 + 1 + 1 which is 1 carry 1, but this time we can throw away the carry and we’re left with 1000 as an answer.

Many thanks to Jahan Ulhaque, Computer Science Student at University of Liverpool for showing me this method.

### Overflow

Overflow is when more bits are stored in the binary value than it could hold.

An example of this is 4 + 7 in 4-bit binary.

```text
0100 + 0101 + 1001
```

The correct result, 9, is too big to fit into 4 bit representation, as the 1 on the front makes it negative 1.

If both inputs to an addition have the same sign, and the output sign is different, overflow has occurred.

Overflow cannot occur if the signs differ.

### **Subtraction in Binary**

Treat this as addition but negate the second operand. So 4–3 is just 4 + \(-3\)

Which is just

```text
0100 + 1101 = 001as we ignore the carry again.
```

## Adding Numbers

Sum of two bits can be obtained by performing XOR \(^\) of the two bits. Carry bit can be obtained by performing AND \(&\) of two bits.

### Sum of 2 bits

```text
0001
xor
0000
=
0001
```

What if we need to carry?

```text
0001
xor
0001
=
0000
```

xor doesn't work. SO we use AND.

### Carries

We can use & and to calculate whether we need carries.

```text
1
and
1
=
1
```

We can then use left shifting, which moves the number 1 to the left.

## Right Shifting

The arithmetic right shift essentially divides by 2. The logical right shift would visually shift the bits.

Imagine a negative number.

In a logical right shift, we shift the bits and put a 0 in the most significant bit. The It is indicated with a `>>>` operator.

On an 8-bit integer \(where the sign bit is the most significant bit\), this would look like the image below \(that I stole out of cracking the coding interview\):

![](../.gitbook/assets/image%20%2832%29.png)

### Left Shifting

Does the opposite of right shifting.

Arithmetic left shifting multiplies by 2.

To multiply a number, a binary shift moves all the digits in the binary number along to the left and fills the gaps after the shift with 0.

It also visually shifts the bits to the left.

```text
00 << 1 = 100
```

### Putting it together for adding 2 numbers without using + symbol

```text
# Python3 Program to add two numbers 
# without using arithmetic operator 
def Add(x, y): 
  
    # Iterate till there is no carry  
    while (y != 0): 
      
        # carry now contains common 
        # set bits of x and y 
        carry = x & y 
  
        # Sum of bits of x and y where at 
        # least one of the bits is not set 
        x = x ^ y 
  
        # Carry is shifted by one so that    
        # adding it to x gives the required sum 
        y = carry << 1
      
    return x 
  
print(Add(15, 32)) 
  
# This code is contributed by 
# Smitha Dinesh Semwal
```

