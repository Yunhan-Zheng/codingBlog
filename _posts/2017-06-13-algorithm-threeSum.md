---
layout: post
title: Three Sum[M]
tags: algorithm leetcode two_pointers array revisit
date: 2017-06-13 17:02:00 -0400
comments: true
---
<a href="https://leetcode.com/problems/3sum/#/description" target="_blank">Three Sum</a>

Example:

Given array S = `[-1, 0, 1, 2, -1, -4]`, a solution set is:

```
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### a+b = -c => two sum - time O(n<sup>2</sup>)

```java
public class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length < 3){
            return res;
        }
        Arrays.sort(nums);
        for (int i = nums.length - 1; i > 1; i--){
            //skip dup
            if (i < nums.length - 1 && nums[i] == nums[i + 1]){
                continue;
            }
            int j = 0, k = i - 1;
            int target = - nums[i];
            twoSum(nums, j, k, target, res);
        }
        return res;
    }
    private void twoSum(
        int[] nums, int start, int end, int target, List<List<Integer>> res){
        while (start < end){
            int sum = nums[start] + nums[end];
            if (sum == target){
                ArrayList<Integer> list = new ArrayList<>();

                list.add(nums[start]);
                list.add(nums[end]);
                list.add(-target);
                
                res.add(list);
                start++;
                while (start < end && nums[start] == nums[start - 1]){
                    start++;
                }
                end--;
                while (start < end && nums[end] == nums[end + 1]){
                    end--;
                }
            } else if (sum > target){
                end--;
            } else {
                start++;
            }
        }
    }
}
```
