---
layout: post
title: Subarray Sum Closest[M]
tags: algorithm jiuzhang subarray sort revisit
date: 2017-06-07 20:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/subarray-sum-closest/" target="_blank">Subarray Sum Closest</a>

Example:

Given [-3, 1, 1, -3, 5], return [0, 2], [1, 3], [1, 1], [2, 2] or [0, 4].

### Prefix Sum

For every integer array, sum[i + 1, j) = sum[0, j) - sum[0, i). sum[0, i) is called `prefix sum`. PrefixSum[0] = 0.

We need to store all prefix sums and sort them. The smallest one is the difference between adjacent two sums.

```java
class PrefixSum{
    int sum;
    int index;
    public PrefixSum(int s, int i) {
        sum = s;
        index = i;
}

// Used for sorting in ascending order of sum
class SortbySum implements Comparator<PrefixSum>{
    public int compare(PrefixSum a, PrefixSum b){
        return a.sum - b.sum;
    }
}
public class Solution {
    public int[] subarraySumClosest(int[] nums) {
        int[] ans = new int[2];
        int n = nums.length;
        if (n == 0){
            return ans;
        }

        if (n == 1){
            ans[0] = 0;
            ans[1] = 0;
            return ans;
        }
        PrefixSum[] sums = new PrefixSum[n+1];
        int pre = 0;
        sums[0] = new PrefixSum(0, 0);
        for (int i = 1; i <= n; i++){
            sums[i] = new PrefixSum(prev + nums[i-1], i);
            prev = sums[i].sum;
        }
        Arrays.sort(sums, new SortbySum());
        int min = Integer.MAX_VALUE;
        for (int i = 1; i <= n; i++){
            if (min > sums[i].sum - sums[i - 1].sum){
                min = sums[i].sum - sums[i - 1].sum;
                int[] tmp = new int[]{sums[i].index - 1, sums[i - 1].index - 1};
                Arrays.sort(tmp);
                ans[0] = tmp[0] + 1;
                ans[1] = tmp[1];
            }
        }
        return ans;
    }
}
```
