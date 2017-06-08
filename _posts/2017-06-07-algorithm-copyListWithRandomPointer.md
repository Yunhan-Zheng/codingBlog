---
layout: post
title: Copy List with Random Pointer[M]
tags: algorithm jiuzhang uber hash_table linked_list revisit
date: 2017-06-07 09:19:00 -0400
comments: true
---
<a href="https://leetcode.com/problems/partition-list/#/description" target="_blank">Copy List with Random Pointer</a>

### Solution with space O(1) and time O(n)

1. Iterate the list and copy node so that it follows its original node. For example, 1->2->2->null becomes 1->1'->2->2'->2->2'->null. 
2. Iterate the list to point the random node for copied nodes.
3. Reconstruct the next relationship so the new copied list is extracted.

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null){
            return null;
        }
        copyNode(head);
        copyRandom(head);
        return split(head);
    }
    private void copyNode(RandomListNode node){
        while (node != null){
            RandomListNode copied = new RandomListNode(node.label);
            copied.next = node.next;
            copied.random = node.random;
            node.next = copied;
            node = node.next.next;
        }
    }
    private void copyRandom(RandomListNode node){
        while (node != null){
            if (node.next.random != null){
                node.next.random = node.random.next;
            }
            node = node.next.next;
        }
    }
    private RandomListNode split(RandomListNode head){
        RandomListNode newHead = head.next;
        while (head != null){
            RandomListNode tmp = head.next;
            head.next = tmp.next;
            head = head.next;
            if (tmp.next != null){
                tmp.next = tmp.next.next;
            }
        }
        return newHead;
    }
}
```

### Solution with space O(n) and time O(n) using HashMap

```java
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null){
            return null;
        }
        HashMap<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode node = head;
        while (node != null){
            map.put(node, new RandomListNode(node.label));
            node = node.next;
        }
        node = head;
        while (node != null){
            map.get(node).next = map.get(node.next);
            map.get(node).random = map.get(node.random);
            node = node.next;
        }
        return map.get(head);
    }
}
```
