---
layout: post
title: Jiuzhang-Closest Number in A Sorted Array
tags: algorithm jiuzhang binary_search revisit
comments: true
---

Q: Given a non-descending array of integers, (e.g., [1, 2, 2, 4, 5, 5],) find the index i that has the closest value to the target integer.

In this example, for target = 7, return 4 or 5; for target = 5, return 4 or 5; for target = 3, return 1 or 2 or 3. If there is no integers in the array, return -1.

Based on Jiuzhang's binary search [template](http://www.jiuzhang.com/solutions/binary-search/), my solution is as follows. 

```java
public int closestNumber(int[] A, int target) {
    if (A == null || A.length == 0){
        return -1;
    }
    int start = 0;
    int end = A.length - 1;
    while (start + 1 < end){
        int mid = start + (end - start) / 2;
        if (A[mid] == target){
            return mid;
        } else if(A[mid] < target){
            start = mid;
        } else {
            end = mid;
        }
    }
    if (A[start] >= target){
        return start;
    }
    if (A[end] <=  target){
        return end;
    }
    return (target - A[start]) >= (A[end] - target) ? end: start;
}
```
While this is an acceptable solution, Jiuzhang has provided a more modular solution.

```java
public int closestNumber(int[] A, int target) {
    if (A == null || A.length == 0) {
        return -1;
    }
    
    int index = firstIndex(A, target);
    if (index == 0) {
        return 0;
    }
    if (index == A.length) {
        return A.length - 1;
    }

    if (target - A[index - 1] < A[index] - target) {
        return index - 1;
    }
    return index;
}

private int firstIndex(int[] A, int target) {
    int start = 0, end = A.length - 1;
    while (start + 1 < end) {
        int mid = start + (end - start) / 2;
        if (A[mid] < target) {
            start = mid;
        } else if (A[mid] > target) {
            end = mid;
        } else {
            end = mid;
        }
    }
    
    if (A[start] >= target) {
        return start;
    }
    if (A[end] >= target) {
        return end;
    }
    return A.length;
}
```

Reference:

[1] https://www.jiuzhang.com/solution/closest-number-in-sorted-array/
[2] https://yisuang1186.gitbooks.io/-shuatibiji/closest_number_in_sorted_array.html
[3] https://www.jiuzhang.com/qa/3538/