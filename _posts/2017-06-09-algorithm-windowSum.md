---
layout: post
title: Window Sum[E]
tags: algorithm jiuzhang amazon subarray array revisit
date: 2017-06-09 10:11:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/window-sum/" target="_blank">Window Sum</a>

Example:

For array [1,2,7,8,5] and moving window size k = 3, return [10,17,20].

```java
public class Solution {
    public int[] winSum(int[] nums, int k) {
        if (nums == null || nums.length < k || k <= 0){
            return new int[0];
        }
        int[] ans = new int[nums.length - k + 1];
        for (int i = 0; i < k; i++){
            ans[0] += nums[i];
        }
        for (int i = 1; i < ans.length; i++){
            ans[i] = ans[i - 1] + nums[i + k - 1] - nums[i - 1];
        }
        return ans;
    }
}
```
