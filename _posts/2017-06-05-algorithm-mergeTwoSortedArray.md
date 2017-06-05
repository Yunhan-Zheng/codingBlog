---
layout: post
title: Merge Two Sorted Array[E]
tags: algorithm jiuzhang sorted_array revisit
date: 2017-06-05 08:39:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/merge-two-sorted-arrays/" target="_blank">Merge Two Sorted Array</a>

Example:

Given A=[1,3,4] and B=[2,4,5,6], return [1,2,3,4,4,5,6]

### Sample solution with time complexity O(n1 + n2) 

This has been optimized for the case that one array is very long and the other one is pretty short.

```java
class Solution {
    public int[] mergeSortedArray(int[] A, int[] B) {
        int[] ans = new int[A.length + B.length];
        int i = 0, j = 0, index = 0;
        while (i < A.length && j < B.length){
            ans[index++] = (A[i] < B[j] ? A[i++] :  B[j++]);
        }
        while (i < A.length){
            ans[index++] = A[i++];
        }
        while (j < B.length){
            ans[index++] = B[j++];
        }
        return ans;
    }
}
```

Another way is to copy one longer array to the answer, and use the same logic in [Merge Sorted Array]({{site.baseurl}}/2017/06/05/algorithm-mergeSortedArray.html).


