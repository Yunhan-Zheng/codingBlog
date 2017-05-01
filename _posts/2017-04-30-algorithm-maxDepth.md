---
layout: post
title: Jiuzhang-Maximum Depth of A Binary Tree
tags: algorithm jiuzhang binary_tree divide_conquer revisit
date: 2017-04-30 11:50:10 -0400
comments: true
---

>Q: Given a binary tree, find its maximum depth.

Example:

Given a binary tree, return 3.
```
            1
          /   \
         2    10
              /  \
             4    7
```
Thoughts:

Find and compare the maximum depth of the left of the root node and that of the right of the root node, choose the larger one and add 1 because of the root.

```java
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```
Jiuzhang has provided another way to solve the problem using the **Traverse** concept.

```java
// version 2: Traverse
public class Solution {
    private int depth;
    
    public int maxDepth(TreeNode root) {
        depth = 0;
        helper(root, 1);
        
        return depth;
    }
    
    private void helper(TreeNode node, int curtDepth) {
        if (node == null) {
            return;
        }
        
        if (curtDepth > depth) {
            depth = curtDepth;
        }
        
        helper(node.left, curtDepth + 1);
        helper(node.right, curtDepth + 1);
    }
}
```

Reference:

http://www.jiuzhang.com/solutions/maximum-depth-of-binary-tree/