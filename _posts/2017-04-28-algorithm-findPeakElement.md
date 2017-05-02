---
layout: post
title: Jiuzhang-Find peak element
tags: algorithm jiuzhang binary_search
date: 2017-04-28 14:10:10 -0400
comments: true
---

>Q: There is an integer array which has the following features:

>The numbers in adjacent positions are different.

>A[0] < A[1] && A[A.length - 2] > A[A.length - 1].

Find the peak position where A[P] > A[P-1] && A[P] > A[P+1].

My solution is as follows.

```java
 public class Solution {
    public int findPeak(int[] A) { 
        //since A is strictly defined, there's no need to check null or length == 0
        int start = 1;
        int end = A.length - 2;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (A[mid] < A[mid - 1]){
                end = mid;
            } else if (A[mid] < A[mid + 1]){
                start = mid;
            } else {
                start = mid; //end = mid also works
            }
        }
        if (A[start] < A[end]){
            return end;
        } else {
            return start;
        }
    }
}
```

Reference:

http://www.lintcode.com/en/problem/find-peak-element/