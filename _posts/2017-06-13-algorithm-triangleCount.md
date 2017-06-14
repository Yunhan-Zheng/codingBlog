---
layout: post
title: Triangle Count[M]
tags: algorithm jiuzhang two_pointers array revisit
date: 2017-06-13 19:02:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/triangle-count/" target="_blank">Triangle Count</a>

Example:

Given array S = [3,3,3,3], return 4. They are:

```
[
  [4(1), 4(2), 4(3)],
  [4(1), 4(2), 4(4)],
  [4(1), 4(3), 4(4)],
  [4(2), 4(3), 4(4)]
]
```

### a + b > c => Sort, right -> left - Time O(nlogn)

```java
public class Solution {
    public int triangleCount(int[] nums) {
        if (nums == null || nums.length < 3){
            return 0;
        }
        Arrays.sort(nums);
        int count = 0;
        for (int i = nums.length - 1; i > 1; i--){
            int j = 0, k = i - 1;
            while (j < k){
                if (nums[j] + nums[k] > nums[i]){
                    count += k - j;
                    k--;
                } else {
                    j++;
                }
            }
        }
        return count;
    }
}
```
