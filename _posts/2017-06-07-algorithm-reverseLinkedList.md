---
layout: post
title: Reverse Linked List[E]
tags: algorithm jiuzhang facebook uber linked_list revisit
date: 2017-06-07 22:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/reverse-linked-list/" target="_blank">Reverse Linked List</a>

Example:

Given a linked list head 1 in 1->2->3 return 3 in 3->2->1.

### Iteration

This is an <a href="https://www.interviewcake.com/concept/java/in-place" target="_blank">in-place</a> solution without creating a new copy of the input. The original input will be altered.

```java
public class Solution {
    public ListNode reverse(ListNode head) {
        ListNode newHead = null;
        while (head != null){
            ListNode next = head.next;
            head.next = newHead;
            newHead = head;
            head = next;
        }
        return newHead;
    }
}
```

### Recursion 

With O(1) space and O(n) time. The idea is to reverse the rest and put the original head in the end.

```java
public class Solution {
    public ListNode reverse(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode newHead = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```