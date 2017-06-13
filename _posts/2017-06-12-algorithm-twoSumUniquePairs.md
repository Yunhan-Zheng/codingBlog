---
layout: post
title: Two Sum - Unique pairs[M]
tags: algorithm jiuzhang array two_pointers revisit
date: 2017-06-12 22:12:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/two-sum-unique-pairs/" target="_blank">Two Sum - Unique pairs</a>

Example:

Given nums = `[1,1,2,45,46,46]` and target = 47, return 2.

### Sort & two pointers - move until next is different

```java
public class Solution {
    public int twoSum6(int[] nums, int target) {
        if (nums == null || nums.length < 2){
            return 0;
        }
        Arrays.sort(nums);
        int count = 0;
        int i = 0, j = nums.length - 1;
        while (i < j){
            int sum = nums[i] + nums[j];
            if (sum == target){
                count++;
                i++;
                j--;
                while (i < j && nums[i] == nums[i - 1]){
                    i++;
                }
                while (i < j && nums[j] == nums[j + 1]){
                    j--;
                }
            } else if (sum > target){
                j--;
            } else {
                i++;
            }
        }
        return count;
    }
}
```

