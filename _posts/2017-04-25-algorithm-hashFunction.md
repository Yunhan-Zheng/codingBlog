---
layout: post
title: Hash Function
tags: algorithm jiuzhang
comments: true
---

Q: Implement a Hash Function that converts a string(or any other type) to an integer. One hash function works this way:

Example: hashcode("abcd") = (ascii(a) * 31<sup>3</sup> + ascii(b) * 31<sup>2</sup> + ascii(c) *31 + ascii(d)) % HASH_SIZE


If one follows the formula to write a solution, it's easy to notice the problem of overflow when the input string is `large`. Therefore, it has to follow below theories regarding the mod operation %.

1. (x * y) % size = (x % size) * (y % size)
2. (x % size) % size = x % size = p
3. (a * 31<sup>n</sup>) % size = (((a * 31) % size ) * 31 ) % size... (n times in total)

The sample solution is as follows.

```java
class Solution {
    public int hashCode(char[] key,int HASH_SIZE) {
        long ans = 0;
        for(int i = 0; i < key.length; i++) {
            ans = (ans * 33 + (int)(key[i])) % HASH_SIZE; 
        }
	return (int)ans;
    }
};
```

In the <a href="https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm" target="_blank">Rabin–Karp algorithm</a>, it uses rolling hash to accelerate the speed of the next hash value in the source string. This is achieved based on a trick.

    hashcode[i+1..i+m] = hashcode[i..i+m-1] - hashcode[i] + hashcode[i+m]

Reference:

<a href="https://www.jiuzhang.com/qa/234/" target="_blank">https://www.jiuzhang.com/qa/234/</a>