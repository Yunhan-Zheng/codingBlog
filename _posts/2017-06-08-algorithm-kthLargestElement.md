---
layout: post
title: Kth Largest Element[M]
tags: algorithm jiuzhang quick_sort sort revisit
date: 2017-06-08 13:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/kth-largest-element/" target="_blank">Kth Largest Element</a>

Assumption: k is always valid, 1 ≤ k ≤ array's length 

Example:

In array [9,3,2,4,8], the 3rd largest element is 4.

### Quick sort - with expectation time complexity O(n), O(1) extra memory.

Based on <a href="https://en.wikipedia.org/wiki/Quickselect" target="_blank">quick select</a>.

<p>
	<img style="width:100%;display:inline-block" alt="quick select time complexity" src="{{site.baseurl}}/public/image/quickSelect.jpeg">
</p>

```java
public class Solution {
    public int kthLargestElement(int k, int[] nums) {
        int n = nums.length;
        int target = n - k;
        quicksort(nums, 0, n - 1, target);
        return nums[target];
    }
    private void quicksort(int[] nums, int start, int end, int target){
        if (start >= end){
            return;
        }
        int mid = start + (end - start) / 2;
        int pivot = choosePivot(nums[mid], nums[start], nums[end]);
        int left = start;
        int right = end;
        while (left <= right){
            while ( nums[left] < pivot){
                left++;
            }
            while ( nums[right] > pivot){
                right--;
            }
            if (left <= right){
                int tmp = nums[left];
                nums[left] = nums[right];
                nums[right] = tmp;
                left++;
                right--;
            }
        }
        if (target < left){
            quicksort(nums, start, left - 1, target);
        } else {
            quicksort(nums, left, end, target);
        }
    }
    private int choosePivot(int a, int b, int c){
        if (a > b){
            if (a < c){
                return a;
            } else if (c > b){
                return c;
            } else {
                return b;
            }
        } else {
            if (a > c){
                return a;
            } else if (c < b){
                return c;
            } else {
                return b;
            }
        }
    }
    
}
```
