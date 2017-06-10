---
layout: post
title: Remove Duplicate Numbers in Array[E]
tags: algorithm jiuzhang amazon hash_set sort two_pointers array revisit
date: 2017-06-09 10:11:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/remove-duplicate-numbers-in-array/" target="_blank">Remove Duplicate Numbers in Array</a>

Example:

Given nums = [1,3,1,4,4,2], we should: 

1. Move duplicate integers to the tail of nums => nums = [1,3,4,2,?,?].
2. Return the number of unique integers in nums => 4.

Note that ? stands for duplicates which we don't care anymore.

### HashSet with time O(n) and space O(n)

```java
public class Solution {
    public int deduplication(int[] nums) {
        if (nums == null || nums.length == 0){
            return 0;
        }
        Set<Integer> set = new HashSet<>();
        set.add(nums[0]);
        for (int i = 1; i < nums.length; i++){
            if (!set.contains(nums[i])){
                set.add(nums[i]);
                nums[set.size() - 1] = nums[i];
            }
        }
        return set.size();
    }
}
```

### Sort first and then compare - with time O(nlogn) and space O(1)

```java
public class Solution {
    public int deduplication(int[] nums) {
        if (nums == null || nums.length == 0){
            return 0;
        }
        Arrays.sort(nums);
        int size = 1;
        for (int i = 1; i < nums.length; i++){
            if (nums[i] != nums[size - 1]){
                nums[size++] = nums[i];
            }
        }
        return size;
    }
}
```