---
layout: post
title: Maximum Subarray[E]
tags: algorithm jiuzhang linkedIn array greedy subarray recursion revisit
date: 2017-06-04 15:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/maximum-subarray/" target="_blank">Maximum Subarray</a>

Example:

Given an array [−2,2,−3,4,−1,2,1,−5,3], the largest sum of a contiguous subarray [4,−1,2,1] is 6.

### Sample solution with time complexity O(n)

The Kadane's algorithm is used to solve this problem. The algorithm sets the first element to be a starting point of maxSoFar and maxEndingHere where maxEndingHere stands for the maximum sum of a subarray that ends with element nums[k]. The algorithm scans through the array. When it scans element nums[i], the maxSoFar is the larger one between the maxSoFar for nums[0] to nums[i - 1] and the maxEndingHere for nums[i].

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];
        for (int i = 1; i < nums.length; i++){
            maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
}
```

### Sample solution in greedy (also with time complexity O(n))
Keep adding elements until sum goes below 0. If sum goes negative, start a new sum (namely, a new subarray).

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0], sum = 0;
        for (int i = 0; i < nums.length; i++){
            sum += nums[i];
            res = Math.max(sum, res);
            sum = Math.max(sum,0);
        }
        return res;
    }
}
```

Reference:

https://discuss.leetcode.com/topic/5000/accepted-o-n-solution-in-java

