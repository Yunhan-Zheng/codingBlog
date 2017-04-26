---
layout: post
title: Leetcode-Hash function
tags: algorithm leetcode easy jiuzhang
comments: true
---

Q: Implement a Hash Function that converts a string(or any other type) to an integer. One hash function works this way:

hashcode("abcd") = (ascii(a) * 33<sup>3</sup> + ascii(b) * 33<sup>2</sup> + ascii(c) *33 + ascii(d)) % HASH_SIZE

Example: input `abcd` and `1007`, hashcode("abcd") = (97* 33<sup>3</sup>  + 98 * 33<sup>2</sup>  + 99 * 33 +100) % 1007 = 988. 

If one follows the formula to write a solution, it's easy to notice the problem of overflow when the input string is `large`. Therefore, it has to follow below theories regarding the mod operation %.

1. (x * y) % size = (x % size) * (y % size)
2. (x % size) % size = x % size = p
3. (a * 33<sup>n</sup>) % size = (((a * 33) % size ) * 33 ) % size... (n times in total)

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

Reference:

<a href="https://www.jiuzhang.com/qa/234/" target="_blank">https://www.jiuzhang.com/qa/234/</a>