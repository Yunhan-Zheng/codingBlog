---
layout: post
title: Intersection of Two Arrays II[E]
tags: algorithm jiuzhang hash_set two_pointers sort follow_up revisit
date: 2017-06-05 14:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/intersection-of-two-arrays-ii/" target="_blank">Intersection of Two Arrays II</a>

Example:

Given nums1 = [1, 2, 3, 2], nums2 = [2, 2, 3], return an array consisting of 2, 2 and 3.

### Using two pointers with time complexity O(nlogn)

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        ArrayList<Integer> temp = new ArrayList<>();
        int i = 0;
        int j = 0;
        while (i < nums1.length && j < nums2.length){
            if (nums1[i] == nums2[j]){
                temp.add(nums1[i]);
                i++;
                j++;
            } else if (nums1[i] > nums2[j]){
                j++;
            } else {
                i++;
            }
        }
        int[] ans = new int[temp.size()];
        int index = 0;
        for (Integer num : temp){
            ans[index++] = num;
        }
        return ans;
    }
}
```

### Using HashMap 

Map stores integers and frequencies.

```java
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        ArrayList<Integer> temp = new ArrayList<Integer>();
        for (Integer n : nums1){
            if (map.containsKey(n)){
                map.put(n, map.get(n) + 1)
            } else {
                map.put(n, 1);
            }
        }
        for (Integer n : nums2){
            if (map.containsKey(n) && map.get(n) > 0){
                temp.add(n);
                map.put(n, map.get(n) - 1);
            }
        }
        int[] ans = new int[temp.size()];
        int i = 0;
        for (Integer num : temp){
            ans[i++] = num; 
        }
        return ans;
    }
}
```

### Follow up

>What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

If only nums2 cannot fit in memory, put all elements of nums1 into a HashMap, read chunks of array that fit into the memory, and record the intersections.

If both nums1 and nums2 are so huge that neither fit into the memory, externally sort them, then read first 2 elements from each array at a time in memory, conduct comparison like that in the first solution and read the next element from the array which has a smaller element taken out before, record intersections.

Reference:

https://discuss.leetcode.com/topic/45992/solution-to-3rd-follow-up-question/2

