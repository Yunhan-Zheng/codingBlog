---
layout: post
title: Reverse Nodes in K-Group[H]
tags: algorithm jiuzhang facebook linked_list revisit
date: 2017-06-08 10:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/reverse-nodes-in-k-group/" target="_blank">Reverse Nodes in K-Group</a>

Example:

Given a linked list head 1 in 1->2->3->4->5

For k = 2, return: 2 in 2->1->4->3->5

For k = 3, return: 3 in 3->2->1->4->5

### Recursion - preappending to a reversed list

```java
public class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode cur = head;
        int count = 0;
        while (cur != null && count < k){
            cur = cur.next;
            count++;
        }
        if (count == k){
            cur = reverseKGroup(cur, k); //after reversing list starting
                                         //from node k+1, return its head
            while (count-- > 0){
                ListNode tmp = head.next; //nodes to be preappended
                head.next = cur;  //preappend
                cur = head; //new head of reversed list
                head = tmp;
            }
        }
        return head;
    }
}
```

### Iteration - last node as a pre node for the next k-length nodes

```java
public class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null || k < 2){
            return head;
        }
        int len = 0;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        while (head != null){
            len++;
            if (len % k == 0){
                pre = reverse(pre, head.next); //逆转区间(pre, head.next)
                head = pre.next;
            } else {
                head = head.next;
            }
        }
        return dummy.next;
    }
    //return last node of the reversed list
    private ListNode reverse(ListNode pre, ListNode next){
        ListNode last = pre.next;
        ListNode cur = last.next;
        while (cur != next){
            last.next = cur.next;
            cur.next = pre.next;
            pre.next = cur;
            cur = last.next;
        }
        return last;
    }
}
```

Reference:

http://www.cnblogs.com/lichen782/p/leetcode_Reverse_Nodes_in_kGroup.html

