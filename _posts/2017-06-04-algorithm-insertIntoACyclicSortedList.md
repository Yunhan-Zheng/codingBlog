---
layout: post
title: Insert into a Cyclic Sorted List
tags: algorithm jiuzhang amazon linkedList revisit
date: 2017-06-04 09:21:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/insert-into-a-cyclic-sorted-list/" target="_blank">Insert into a Cyclic Sorted List</a>

Example:

Given a node 3 from list 1->3->5, and a value 4, return the new inserted node so that 5->1->3->4

Since the list is cyclic, it's easy to think about looping the list and find where the new node fits in. A ListNode prev is needed to refer to the previous node of current node in the list. 

### Sample solution

```java
public class Solution {
    /**
     * @param node a list node in the list
     * @param x an integer
     * @return the inserted new list node
     */
    public ListNode insert(ListNode node, int x) {
        ListNode newNode = new ListNode(x);
        if (node == null){
            newNode.next = newNode;
            return newNode;
        }
        ListNode p = node;
        ListNode prev = null;
        do {
            prev = p;
            p = p.next;
            if (x >= prev.val && x <= p.val){
                break;
            }
            if (prev.val > p.val && (x < p.val || x > prev.val)){
                break;
            }
        } while (p != node);
    }
    prev.next = newNode;
    newNode.next = p;
    return newNode;
}
```