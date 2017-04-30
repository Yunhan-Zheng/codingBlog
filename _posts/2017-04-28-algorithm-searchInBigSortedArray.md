---
layout: post
title: Jiuzhang-Search in a big sorted array
tags: algorithm jiuzhang binary_search revisit
comments: true
---

>Q: Given a big sorted array with positive integers sorted by ascending order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by ArrayReader.get(k). Find the **first** index of a target number. Your algorithm should be in **O(log k)**, where k is the first index of the target number.

>Return -1, if the number doesn't exist in the array.
>If you accessed an inaccessible index (outside of the array), ArrayReader.get will return 2,147,483,647.

The sample solution is as follows.

```java
/**
 * Definition of ArrayReader:
 * 
 * class ArrayReader {
 *      // get the number at index, return -1 if index is less than zero.
 *      public int get(int index);
 * }
 */
 public class Solution {
    public int searchBigSortedArray(ArrayReader reader, int target) {
        int index = 1;
        while (reader.get(index -1) < target){
            index *= 2; 
        }
        int start = 0;
        int end = index - 1;
        while (start + 1 < end){
            int mid = start + (end - start) / 2;
            if (reader.get(mid) < target){
                start = mid;
            } else {
                end = mid;
            }
        }
        if (reader.get(start) == target){
            return start;
        }
        if (reader.get(end) == target){
            return end;
        }
        return -1;
    }
}
```

Afterthoughts:

This problem reminds me of a brain teaser [The Two Egg Problem](http://datagenetics.com/blog/july22012/index.html).

Reference:

http://www.lintcode.com/en/problem/search-in-a-big-sorted-array/