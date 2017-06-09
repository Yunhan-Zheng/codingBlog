---
layout: post
title: Median of Two Sorted Arrays[H]
tags: algorithm jiuzhang zenefits uber google sorted_array array divide_conquer revisit
date: 2017-06-09 09:11:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/median-of-two-sorted-arrays/" target="_blank">Median of Two Sorted Arrays</a>

Example:

Given A=[1,2,3,4,5,6] and B=[2,3,4,5], the median is 3.5.

Given A=[1,2,3] and B=[4,5], the median is 3.

### Shrink the problem by half - O(log (m+n))

In general, we can find the k<sup>th</sup> smallest number of a combined array and pass the median index to find the result, or compute if m + n is even. 

However, to satisfy the requirement time complexity O(log (m + n)), we need to use time O(1) to break down a problem of T(n) to T(n/2). 

In order to do that, we can find the (k/2)<sup>th</sup> in each array and compare which one is smaller. Say the index is s in array1. Numbers in array1[0, s] are definately k/2 numbers that are smaller than the median. Therefore, we then need to find k/4 smaller numbers. 

When k = 1, we will return the smaller one between array1[start1] and array2[start2].

<p>
	<img style="width:100%;display:inline-block" alt="T(n) = T(n/2) + O(1)" src="{{site.baseurl}}/public/image/shrinkByHalfOfK.jpeg">
</p>

```java
public class Solution {
    public double findMedianSortedArrays(int[] A, int[] B) {
        int n = A.length + B.length;
        if (n % 2 == 1){
            return findKth(A, 0, B, 0, n/2 + 1);
        } else {
            return (
                findKth(A, 0, B, 0, n/2) + findKth(A, 0, B, 0, n/2 + 1)
            ) / 2.0;
        }
    }
    private int findKth(int[] A, int startA, int[] B, int startB, int k){
        if (startA >= A.length){
            return B[startB + k - 1];
        }
        if (startB >= B.length){
            return A[startA + k - 1];
        }
        if (k == 1){
            return Math.min(A[startA], B[startB]);
        }
        int A_key = startA + k/2 - 1 < A.length ? A[startA + k/2 - 1] :                 Integer.MAX_VALUE;
        int B_key = startB + k/2 - 1 < B.length ? B[startB + k/2 - 1] :                 Integer.MAX_VALUE;
        if (A_key < B_key){
            return findKth(A, startA + k/2, B, startB, k - k/2);
        }
        return findKth(A, startA, B, startB + k/2, k - k/2);
    }
}
```
