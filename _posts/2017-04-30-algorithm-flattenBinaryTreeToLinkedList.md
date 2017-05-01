---
layout: post
title: Jiuzhang-Flatten Binary Tree to Linked List
tags: algorithm jiuzhang binary_tree divide_conquer revisit resulttype
date: 2017-04-30 20:20:14 -0400
comments: true
---

>Q: Flatten a binary tree to a fake "linked list" in pre-order traversal.

Example:

```
              1
               \
     1          2
    / \          \
   2   5    =>    3
  / \   \          \
 3   4   6          4
                     \
                      5
                       \
                        6
```

Here we use the right pointer in TreeNode as the next pointer in ListNode.

```java
public class Solution {
    private TreeNode lastNode = null;
    public void flatten(TreeNode root) {
        if (root == null){
            return;
        }
        if (lastNode != null){
            lastNode.left = null;
            lastNode.right = root;
        }
        lastNode = root;
        TreeNode right = root.right;
        flatten(root.left);
        flatten(right); //因为经过上一步后，root.right变成root.left, 
                        //所以要用right这个指针保存root原来的right
    }
}
```

Reference:

http://www.lintcode.com/en/problem/flatten-binary-tree-to-linked-list/