---
layout: post
title: Longest Palindromic Substring
tags: algorithm leetcode string revisit
date: 2017-06-02 20:10:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/longest-palindromic-substring/" target="_blank">Longest Palindromic Substring</a>

Example:

Given a string "abcdzdcab", return "cdzdc".

Say I have a string "øøbabøøøøøc" where ø stands for any letter. The current longest length is 3 which corresponds to "bab". When I move to the right of the original string, I only need check for possible length values that are 1 or 2 more than the current longest length.

Why?

Assume øøøøøc is the longest which has length of 6 (more than 3 + 2). Cutting off the head and tail gives øøøø in the middle. Since it is also palindromic and its length is 4, it violates the first assumption that 3 is the current longest length. 

```java
public class Solution {
    public String longestPalindrome(String s) {
        int curLen = 0;
        int start = -1;
        char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; i++){
            if (isPalindrome(arr, i - curLen - 1, i)){
                start = i - curLen - 1;
                curLen += 2;
            } else if (isPalindrome(arr, i - curLen, i)){
                start = i - curLen;
                curLen += 1;
            }
        }
        return new String(arr, start, curLen);
    }
    private boolean isPalindrome(char[] array, int start, int end) {
        if (start < 0){
            return false;}
        while (start < end){
            if (array[start++] != array[end--]){
                return false;
            }
        }
        return true;
    }
}
```

