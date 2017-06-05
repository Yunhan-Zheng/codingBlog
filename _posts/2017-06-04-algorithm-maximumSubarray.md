---
layout: post
title: Maximum Subarray[E]
tags: algorithm jiuzhang linkedIn array greedy subarray divide_conquer recursion revisit
date: 2017-06-04 15:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/maximum-subarray/" target="_blank">Maximum Subarray</a>

Example:

Given an array [−2,2,−3,4,−1,2,1,−5,3], the largest sum of a contiguous subarray [4,−1,2,1] is 6.

### Kadane's algorithm with time complexity O(n)

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

### Greedy (also with time complexity O(n))
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

### Divide and Conquer with time complexity O(nlogn)
Credited to [porker2008](https://discuss.leetcode.com/topic/426/how-to-solve-maximum-subarray-by-using-the-divide-and-conquer-approach/2), the steps in this solution are as follows.

```java
public class Solution {
    public int maxSubArray(int nums[]) {
        int n = nums.length;
        if (n == 0){
            return 0;
        }
        return maxSubArrayHelper(nums, 0, n - 1);
    }
    
    private int maxSubArrayHelper(int A[], int left, int right) {
        if (right == left){
            return A[left];
        }
        int middle = (left + right) / 2;
        int leftAns = maxSubArrayHelper(A, left, middle);
        int rightAns = maxSubArrayHelper(A, middle + 1, right);
        int leftmax = A[middle];
        int rightmax = A[middle + 1];
        int temp = 0;
        for (int i = middle; i >= left; i--){
            temp += A[i];
            if (temp > leftmax){
                leftmax = temp;
            }
        }
        temp = 0;
        for (int i = middle + 1; i <= right; i++){
            temp += A[i];
            if (temp > rightmax){
                rightmax = temp;
            }
        }
        return Math.max(Math.max(leftAns, rightAns), leftmax + rightmax);
    }
}
```

Reference:

https://discuss.leetcode.com/topic/5000/accepted-o-n-solution-in-java

https://discuss.leetcode.com/topic/426/how-to-solve-maximum-subarray-by-using-the-divide-and-conquer-approach

