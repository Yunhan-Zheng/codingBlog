---
layout: post
title: Linked List Cycle[M]
tags: algorithm jiuzhang linked_list two_pointers revisit
date: 2017-06-06 23:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/subarray-sum/" target="_blank">Linked List Cycle</a>

Example:

Given -21->10->4->5, tail connects to node index 1, return true.

### Use two pointers

```java
public class Solution {
    public boolean hasCycle(ListNode head) { 
        if (head == null || head.next == null){
            return false;
        }
        ListNode node1 = head.next;
        ListNode node2 = head;
        while (node1 != node2){
            if (node1 == null || node1.next == null){
                return false;
            }
            node1 = node1.next.next;
            node2 = node2.next;
        }
        return true;
    }
}
```


