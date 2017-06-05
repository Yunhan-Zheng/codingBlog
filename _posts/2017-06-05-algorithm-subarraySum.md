---
layout: post
title: Subarray Sum[E]
tags: algorithm jiuzhang hash_table subarray revisit
date: 2017-06-05 08:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/subarray-sum/" target="_blank">Subarray Sum</a>

Example:

Given [-3, 1, 2, -3, 4], return the index of the head and tail of subarray whose sum is 0: [0, 2] or [1, 3].

### Using HashMap

Map stores sum[0, i]. If sum[0, j] == sum[0, i], then sum[i + 1, j], inclusive, is 0.

```java
public class Solution {
    public ArrayList<Integer> subarraySum(int[] nums) {
        ArrayList<Integer> res = new ArrayList<>();
        int n = nums.length;
        int sum = 0;

        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        map.put(0, -1);
        for (int i = 0; i < n; i++){
            sum += nums[i];
            if (map.containsKey(sum)){
                res.add(map.get(sum) + 1);
                res.add(i);
                return res;
            }
            map.put(sum, i);
        }
        return res;
    }
}
```


