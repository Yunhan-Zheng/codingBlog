---
layout: post
title: Partition List[M]
tags: algorithm leetcode linked_list two_pointers revisit
date: 2017-06-06 09:19:00 -0400
comments: true
---
<a href="https://leetcode.com/problems/partition-list/#/description" target="_blank">Partition List</a>

Example:

Given head node 1 in 1->4->3->2->5->2->null and a value x = 3, return head node such that 1->2->2->4->3->5->null.

The idea is to separate the list into two lists. One with all nodes' values **less than** x and the rest in another one. Then concatenate the two.

```java
public class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        ListNode cur1 = leftDummy, cur2 = rightDummy;
        while (head != null){
            if (head.val < x){
                cur1.next = head;
                cur1 = cur1.next;
            } else {
                cur2.next = head;
                cur2 = cur2.next;
            }
            head = head.next;
        }
        cur2.next = null;
        cur1.next = rightDummy.next;
        return leftDummy.next;
    }
}
```


