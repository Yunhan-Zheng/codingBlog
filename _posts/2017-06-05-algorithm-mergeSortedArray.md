---
layout: post
title: Merge Sorted Array[E]
tags: algorithm jiuzhang facebook sorted_array revisit
date: 2017-06-05 08:39:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/merge-sorted-array/" target="_blank">Merge Sorted Array</a>

Example:

Given A = [1, 6, 9, empty, empty] and B = [4, 8], after merge, A will be [1, 4, 6, 8, 9].

To avoid moving all array A elements when inserting one B element, it's better to start comparing the biggest ones.

```java
class Solution {
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        int index = m + n - 1;
        int i = m - 1;
        int j = n - 1;
        while (i >= 0 || j >= 0){
            if (i < 0){
                A[index--] = B[j--];
            } else if (j < 0) {
                break;
            } else if (A[i] > B[j]) {
                A[index--] = A[i--];
            } else {
                A[index--] = B[j--];
            }
        }
    }
}
```


