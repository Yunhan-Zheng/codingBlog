---
layout: post
title: Jiuzhang-Lowest Common Ancestor
tags: algorithm jiuzhang binary_tree divide_conquer revisit
date: 2017-05-01 23:05:00 -0400
comments: true
---

>Q: Given the root and two nodes *in* a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes. Assume at least two nodes exist in the tree. 

>The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

Example:

Given a binary tree below, LCA(4, 13) = 13, and LCA(7, -2) = -1.
```
            -1
            /  \
           7   13
              /  \
             4    -2
```
Thoughts:

1. If one of the nodes is a root of the other, return the root node.
2. If found both in the left and the right tree, return the root.
3. If not found in left/right subtree, return the right/left root.
4. If didn't find any of the node, return null.

```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null || A == root || B == root){
            return root;
        }
        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);
        if (left != null && right != null){
            return root;
        }
        if (left != null){
            return left;
        }
        if (right != null){
            return right;
        }
        return null;
    }
}    
```

Reference:

http://www.lintcode.com/en/problem/lowest-common-ancestor/