---
layout: post
title: Intersection of Two Arrays[E]
tags: algorithm jiuzhang hash_set two_pointers sort binary_search revisit
date: 2017-06-05 13:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/intersection-of-two-arrays/" target="_blank">Intersection of Two Arrays</a>

Example:

Given nums1 = [1, 2, 3, 1], nums2 = [2, 2, 3], return [2, 3] or [3, 2].

### Using two pointers with time complexity O(nlogn)

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        Set<Integer> set = new HashSet<>();
        int i = 0;
        int j = 0;
        while (i < nums1.length && j < nums2.length){
            if (nums1[i] == nums2[j]){
                set.add(nums1[i]);
                i++;
                j++;
            } else if (nums1[i] > nums2[j]){
                j++;
            } else {
                i++;
            }
        }
        int[] ans = new int[set.size()];
        int index = 0;
        for (Integer num : set){
            ans[index++] = num;
        }
        return ans;
    }
}
```

### Binary search with time complexity O(nlogn)

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums2);
        for (Integer num : nums1) {
            if (binarySearch(nums2, num)) {
                set.add(num);
            }
        }
        int i = 0;
        int[] ans = new int[set.size()];
        for (Integer num : set) {
            ans[i++] = num;
        }
        return ans;
    }
    private boolean binarySearch(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (nums[mid] == target) {
                return true;
            }
            if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }
        return false;
    }
}
```

### Using HashSet with time complexity O(n)

One hash set to store unique numbers in nums1, the other one to store the common one(s) in nums2.

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Set<Integer> intersection = new HashSet<>();
        for (Integer n : nums1){
            set.add(n);
        }
        for (Integer n : nums2){
            if (set.contains(n)){
                intersection.add(n);
            }
        }
        int[] ans = new int[intersection.size()];
        int i = 0;
        for (Integer num : intersection){
            ans[i++] = num; 
        }
        return ans;
    }
}
```

In Java 8, a new package java.util.stream which supports functional-style operations on streams of elements, similar to SQL statements.

[Ericxliu](https://discuss.leetcode.com/user/ericxliu) provided below solution using `stream` which I need to be familiar with.

```java
Set<Integer> set = Arrays.stream(nums2).boxed().collect(Collectors.toSet());
return Arrays.stream(nums1).distinct().filter(e-> set.contains(e)).toArray();
```
