---
layout: post
title: Rotate String[E]
tags: algorithm jiuzhang array revisit
date: 2017-06-12 15:02:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/rotate-string/" target="_blank">Rotate String</a>

Example:

Given an array `[a,b,c,d,e,f]` and 3, the array is rotated to `[d,e,f,a,b,c]`.

### Reverse - time complexity O(n) and space complexity O(1)

```java
public class Solution {
    public void rotate(char[] ch, int k) {
       if (ch == null || ch.length <= 1 || k <= 0){
           return;
       } 
       k %= ch.length;
       reverse(ch, 0, ch.length - 1);
       reverse(ch, 0, k - 1);
       reverse(ch, k, ch.length - 1);
    }
    private void reverse(char[] ch, int start, int end){
        char tmp;
        while (start < end){
            tmp = ch[start];
            ch[start] = ch[end];
            ch[end] = tmp;
            start++;
            end--;
        }
    }
}
```

### Solution with time complexity O(n) and space complexity O(k % ch.length) 

```java
public class Solution {
    public void rotate(char[] ch, int k) {
        if (ch == null || ch.length <= 1 || k <= 0){
           return;
        }
        int offset = k % nums.length;
        int[] tmp = new int[offset];
        for (int i = 0; i < offset; i++){
            tmp[i] = ch[ch.length - offset + i];
        }
        for (int i = ch.length - offset - 1; i >= 0; i--){
            ch[i + offset] = ch[i];
        }
        for (int i = 0; i < offset; i++){
            ch[i] = tmp[i];
        }
    }
}
```