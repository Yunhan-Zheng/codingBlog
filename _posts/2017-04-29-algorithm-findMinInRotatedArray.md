---
layout: post
title: Jiuzhang-Find Minimum in Rotated Sorted Array
tags: algorithm jiuzhang binary_search
comments: true
---

>Q: Suppose a sorted array is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2). Assume no duplicate exists in the array.

>Find the minimum element.

Thoughts:

Using visualization sometimes will help significantly.

<p>
	<img alt="rotated array" src="{{site.baseurl}}/public/image/findMinInRotated.jpeg">
</p>

After finding out the mid point, compare it with the **end** value to decide whether to move start to mid or move end to mid.

My solution is as follows.

```java
public class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length == 0){
            return -1;
        }
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (nums[mid] < nums[end]){
                end = mid;
            } else {
                start = mid;
            }
        }
        if (nums[start] < nums[end]){
            return nums[start];
        }
        return nums[end];
    }
}
```
Another problem [Search in Rotated Sorted Array](http://www.lintcode.com/en/problem/search-in-rotated-sorted-array/) can be solved based on this problem. Once the rotate point is found, the left and right side of it are two sorted arrays.

Reference:

http://www.lintcode.com/en/problem/find-minimum-in-rotated-sorted-array/