---
layout: post
title: Two Sum - Input array is sorted[M]
tags: algorithm jiuzhang amazon array two_pointers sort revisit
date: 2017-06-12 22:02:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/two-sum-input-array-is-sorted/" target="_blank">Two Sum - Input array is sorted</a>

Example:

Given numbers = `[2, 7, 11, 15]`, target=9, return indexes `[0,1]`.

### Sort & two pointers - time O(nlogn) and space O(1)

```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0, j = nums.length - 1;
        while (i < j){
            if (nums[i] + nums[j] > target){
                j--;
            } else if (nums[i] + nums[j] < target){
                i++;
            } else {
                int[] ans = {i, j};
                return ans;
            }
        }
        int[] ans = {};
        return ans; 
    }     
}
```
