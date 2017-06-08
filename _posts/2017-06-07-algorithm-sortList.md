---
layout: post
title: Sort List[M]
tags: algorithm jiuzhang linked_list revisit
date: 2017-06-07 18:19:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/sort-list/" target="_blank">Sort List</a>

It's asking for solution with O(nlogn) time and constant space. When it comes to time O(nlogn) for sorting, the most common solution will be either merge sort or quick sort.

### Merge Sort

```java
public class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode mid = findMid(head);
        ListNode right = sortList(mid.next);
        mid.next = null;
        ListNode left = sortList(head);

        return merge(left, right);
    }
    private ListNode findMid(ListNode head){
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
    private ListNode merge(ListNode h1, ListNode h2){
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (h1 != null && h2 != null){
            if (h1.val < h2.val){
                tail.next = h1;
                h1 = h1.next;
            } else {
                tail.next = h2;
                h2 = h2.next;
            }
            tail = tail.next;
        }
        if (h1 != null){
            tail.next = h1;
        }
        if (h2 != null){
            tail.next = h2;
        }
        return dummy.next;
    }
}
```

### Quick Sort

```java
public class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode mid = findMid(head);
        ListNode leftDummy = new ListNode(0), leftTail = leftDummy;
        ListNode midDummy = new ListNode(0), midTail = midDummy;
        ListNode rightDummy = new ListNode(0), rightTail = rightDummy;
        while (head != null){
            if (head.val < mid.val){
                leftTail.next = head;
                leftTail = head;
            } else if (head.val > mid.val){
                rightTail.next = head;
                rightTail = head;
            } else {
                midTail.next = head;
                midTail = head;
            }
            head = head.next;
        }
        leftTail.next = null;
        midTail.next = null;
        rightTail.next = null;
        
        ListNode left = sortList(leftDummy.next);
        ListNode right = sortList(rightDummy.next);

        return concat(left, midDummy.next, right);
    }
    private ListNode findMid(ListNode head){
        ListNode slow = head, fast = head.next;
        while (fast != null && fat.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    private ListNode concat(ListNode left, ListNode mid, ListNode right){
        ListNode dummy = new ListNode(0), tail = dummy;
        tail.next = left;
        tail = getTail.tail(tail);
        tail.next = mid;
        tail = getTail.tail(tail);
        tail.next = right;
        
        return dummy.next;
    }
    private ListNode getTail(ListNode head){
        while (head.next != null){
            head = head.next;
        }
        return head;
    }
}
```
