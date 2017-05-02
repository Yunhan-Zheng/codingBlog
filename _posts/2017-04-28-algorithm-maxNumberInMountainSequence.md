---
layout: post
title: Jiuzhang-Maximum Number in A Mountain Sequence
tags: algorithm jiuzhang binary_search revisit
date: 2017-04-28 13:20:14 -0400
comments: true
---

Q: Given a mountain sequence of n integers which first increase and then decrease, find the mountain top.

Example:

Given [10,8,5], return 10; Given [1,3,8,4,3], return 8. 

The sample solution is as follows.

```java
public class Solution {
    public int mountainSequence(int[] nums) {
        if (nums ==  null || nums.length == 0){
            return -1;
        }
        int left = 0;
        int right = nums.length - 1;
        while (left + 1 < right){
            int mid = left + (right - left) / 2;
            if (nums[mid - 1] < nums[mid]){
                left = mid;
            } else {
                right = mid;
            }
        }
        return Math.max(nums[left], nums[right]);
    }
}
```

Reference:

http://www.lintcode.com/en/problem/maximum-number-in-mountain-sequence/