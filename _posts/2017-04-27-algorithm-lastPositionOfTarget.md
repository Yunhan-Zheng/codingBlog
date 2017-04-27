---
layout: post
title: Leetcode-Last position of target
tags: algorithm leetcode jiuzhang binary_search
comments: true
---

Q: Given a non-descending array of integers, (e.g., [1, 2, 2, 4, 5, 5],) find the last position of a target integer.

In this example, for target = 2, return 2; for target = 5, return 5; for target = 6, return -1.

My solution is as follows. 

```java
public class Solution {
    public int lastPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0){
            return -1;
        }
        int start = 0;
        int end = nums.length - 1;
        int last = -1;
        while (start < end){
            int mid = (start + end) / 2;
            if (nums[mid] == target){
                last = mid;
                start = mid + 1;
            } else if (nums[mid] > target){
                end = mid - 1;
            } else if (nums[mid] < target){
                start = mid + 1;
            }
        }
        if (nums[start] == target){
            last = start;
        }
        return last;
    }
}
```
Here, because I used `last` to store the occurence and set `start = mid + 1`, there won't be infinite loop, which will happen to below solution.

```java
public int lastPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                start = mid;  //Set start = mid to remember the occurence.
                            //However, it will cause infinite loop 
                            //where start < end always is true.
            } else if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        return -1;
    }
```

There is a template from Jiuzhang<sup>[1]</sup> for binary search to avoid the infinite while loop. I suggest using this one for binary search problems.

```java
public int findPosition(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        
        int start = 0, end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
```

Reference:

[1] http://www.jiuzhang.com/solutions/binary-search/