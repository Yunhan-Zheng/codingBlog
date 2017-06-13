---
layout: post
title: Valid Palindrome[E]
tags: algorithm jiuzhang uber facebook zenefits two_pointers string revisit
date: 2017-06-12 10:02:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/valid-palindrome/" target="_blank">Valid Palindrome</a>

Example:

Given "Was it a cat I saw?", return `true`.


```java
public class Solution {
    public boolean isPalindrome(String s) {
       if (s == null || s.length() <= 1){
            return true;
        }
        int head = 0;
        int tail = s.length() - 1;
        while (head < tail){
            while (head < tail && !Character.isLetterOrDigit(s.charAt(head))){
                head++;
            }
            while (head < tail && !Character.isLetterOrDigit(s.charAt(tail))){
                tail--;
            }
            if (Character.toLowerCase(s.charAt(head)) == Character.toLowerCase(s.charAt(tail))){
                head++;
                tail--;
            } else {
                return false;
            }
        }
        return true; 
    }
}
```
