---
layout: post
title: Bit hacks
tags: bit_manipulation hacks
comments: true
---

I've always been fascinated by how an algorithm problem can be solved using bit hacks in a few lines of code.

Here's a blog [post](http://www.catonmat.net/blog/low-level-bit-hacks-you-absolutely-must-know/) by Peter Krumins, which described 10 bit hacks using bitwise operations<sup>[1]</sup>:

```text
&   -  bitwise and
|   -  bitwise or
^   -  bitwise xor
~   -  bitwise not
<<  -  bitwise shift left
>>  -  bitwise shift right
```

[1] : For more examples using bitwise operations, please refer to <a href='https://www.tutorialspoint.com/java/java_basic_operators.htm' target='_blank'>java basic operators</a>.

### 1. Even or Odd  <a id="evenOrOdd"></a>
    if ((x & 1) == 0) {
      x is even
    }
    else {
      x is odd
    }

1 in binary notation is `00000001`. It's a mask which covers all digits of X with 0s except the smallest one. Since converting binary to decimal is using 2<sup>n</sup> where the only odd number comes from the smallest bit, it is easy to understand this bit hack.

Note that this also works for negative decimals. To find the negative value of a given number in two's complement representation is to invert all bits(8) and add one.
 
### 2. n-th bit set?
    if (x & (1<<n)) {
      n-th bit is set
    }
    else {
      n-th bit is not set
    }

Based on the first bit hack, we know whether the smallest bit is set or not. Following the same logic, by left shifting 1 to the n<sub>th</sub> bit and AND-ing with X will check the n<sub>th</sub>(0-based) bit.

Example: 

12<sub>(10)</sub> = 00001100<sub>(2)</sub>; 1<<3 = `00001000`; 
12 & (1<<3) = `00001100` & `00001000`. 

So we know what value is on 3th bit(from right to left and start from 0).

### 3. Set the n-th bit
    y = x | (1<<n)

When OR-ing X with a mask `00..1..0` where n<sub>th</sub> bit is 1, other bits will not change except the n<sub>th</sub> bit being always 1 after the OR-ing.

### 4. Unset the n-th bit
    y = x & ~(1<<n)

The main function is done by `~(1<<n)` which sets all bits to **1** except the n<sub>th</sub> bit being **0**. 

### 5. Toggle the n-th bit
    y = x ^ (1<<n)

This is called toggle because 

1)if the n<sub>th</sub> bit is 1, XOR-ing it with 1 will change it to 0; 

2)if the n<sub>th</sub> bit is 0, XOR-ing it with 1 will change it to 1.

Example: `temp ^= 1 << bitIndex` in the privous post. Say temp = 00000011, bitIndex = 0, XOR-ing clears the bitIndex.

      00000011
    ^ 00000001 
      -------- 
      00000010 

### 6. Turn off the rightmost 1-bit
    y = x & (x-1)

There are two scenarios:

>1. The value has the rightmost 1 bit. In this case subtracting one from it sets all the lower bits to one and changes that rightmost bit to 0 (so that if you add one now, you get the original value back). This step has masked out the rightmost 1-bit and now AND-ing it with the original value zeroes that rightmost 1-bit out.
2. The value has no rightmost 1 bit (all 0). In this case subtracting one underflows the value (as it's signed) and sets all bits to 1. AND-ing all zeroes with all ones produces 0.

Some examples:

      10000000    (x = -128)
    & 01111111    (x-1 = 127 (with overflow))
      --------
      00000000

      01011000    (x)
    & 01010111    (x-1)
      --------
      01010000

      00000000    (x = no rightmost 1-bits)
    & 11111111    (x-1)
      --------
      00000000

### 7. Isolate the rightmost 1-bit.
    y = x & (-x)

Why?

> In two's complement system -x is the same as ~x+1. Now let's examine the two possible cases:
1. There is a rightmost 1-bit bi. In this case let's pivot on this bit and divide all other bits into two flanks - bits to the right and bits to the left. Remember that all the bits to the right bi-1, bi-2 ... b0 are 0's (because bi was the rightmost 1-bit). And bits to the left are the way they are. Call them bi+1, ..., bn.
Now, to get -x, we first do ~x which turns bit bi into 0, bits bi-1 ... b0 into 1s, and inverts bits bi+1, ..., bn, and then we add 1 to this result.
Since bits bi-1 ... b0 are all 1's, adding one makes them carry this one all the way to bit bi, which is the first zero bit.
If we put it all together, the result of calculating -x is that bits bi+1, ..., bn get inverted, bit bi stays the same, and bits bi-1, ..., b0 are all 0's.
Now, AND-ing x with -x makes bits bi+1, ..., bn all 0, leaves bit bi as is, and sets bits bi-1, ..., b0 to 0. Only one bit is left, it's the bit bi - the rightmost 1-bit.
2. There is no rightmost 1-bit. The value is 0. The negative of 0 in two's complement is also 0. 0&0 = 0. No bits get turned on.

Some examples:

      10111100  (x)
    & 01000100  (-x)
      --------
      00000100

### 8. Right propagate the rightmost 1-bit.
    y = x | (x-1)

Some examples:

      10111100  (x)
    | 10111011  (x-1)
      --------
      10111111

Exception:

      00000000  (x)
    | 11111111  (x-1)
      --------
      11111111

### 9. Isolate the rightmost 0-bit
    y = ~x & (x+1)

Some examples:

      10111100  (x)
      --------
      01000011  (~x)
    & 10111101  (x+1)
      --------
      00000001

      00000000  (x)
      --------
      11111111  (~x)
    & 00000001  (x+1)
      --------
      00000001

### 10. Turn on the rightmost 0-bit
    y = x | (x+1)

Some examples:

      10111100  (x)
    | 10111101  (x+1)
      --------
      10111101

      01110111  (x)
    | 01111000  (x+1)
      --------
      01111111

Reference:

<a href='http://www.catonmat.net/blog/low-level-bit-hacks-you-absolutely-must-know/' target='_blank'>http://www.catonmat.net/blog/low-level-bit-hacks-you-absolutely-must-know/</a>
