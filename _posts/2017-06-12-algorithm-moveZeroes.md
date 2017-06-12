---
layout: post
title: Move Zeroes[E]
tags: algorithm jiuzhang two_pointers array revisit
date: 2017-06-12 09:02:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/move-zeroes/" target="_blank">Move Zeroes</a>

Example:

Given nums = [0, 1, 0, 3, 12], after calling the function, nums should be [1, 3, 12, 0, 0].

Must do this **in-place** without making a copy of the array.

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length <= 1){
            return;
        }
        for (int i = 0; i < nums.length; i++){
            for (int j = i + 1; j < nums.length; j++){
                if (nums[i] == 0 && nums[j] != 0){
                    swap(nums, i, j);
                }
            }
        }
    }
    private void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
