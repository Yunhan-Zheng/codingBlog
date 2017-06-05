---
layout: post
title: Merge Two Sorted Lists[E]
tags: algorithm jiuzhang linkedIn linked_list resursion revisit
date: 2017-06-04 13:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/merge-two-sorted-lists/" target="_blank">Merge Two Sorted Lists</a>

Example:

Given 1 in 1->3->8->11->15->null, and 2 in 2->4->null , return 1 in  1->2->3->4->8->11->15->null.

### Sample solution with recursion

```java
public class Solution {
    /**
     * @param ListNode l1 is the head of the linked list
     * @param ListNode l2 is the head of the linked list
     * @return: ListNode head of linked list
     */
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) return l2;
        if (l2 == null) return l1;
        if (l1.val < l2.val){
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
}
```

### Sample solution with a new list

A dummy node is created to track the head of the new list

```java
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode last = dummy; //记录新linked list最后位置
        while (l1 != null && l2 != null){
            if (l1.val < l2.val){
                last.next = l1;
                l1 = l1.next;
            } else {
                last.next = l2;
                l2 = l2.next;
            }
            last = last.next;
        }
        if (l1 != null){
            last.next = l1;
        } else {
            last.next = l2;
        }
        return dummy.next;
    }
}
```