---
layout: post
title: Jiuzhang-Binary Tree Longest Consecutive Sequence
tags: algorithm jiuzhang binary_tree divide_conquer revisit
date: 2017-05-05 14:01:00 -0400
comments: true
---

>Q: Given a binary tree, find the length of the longest consecutive sequence path.

>The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

Example:

Given a binary tree below, longest consecutive sequence path is -1-0, so return 2.
```
            -1
            /  \
           7   0
              /  \
             2    -2
```


To find the longest consecutive path's length for the whole tree, we can use Divide & Conquer to narrow the problem to its left and right subtree.

```java
public class Solution {
    private int longest;
    public int longestConsecutive(TreeNode root) {
        longest = 0;
        helper(root);
        return longest;
    }
    public int helper(TreeNode root){
        if (root == null){
            return 0;
        }
        int subtreeLongest = 1; // there has been a root.
        int left = helper(root.left);
        int right = helper(root.right);
        if (root.left != null && root.left.val == root.val + 1){
            subtreeLongest = Math.max(subtreeLongest, left + 1);
        }
        if (root.right != null && root.right.val == root.val + 1){
            subtreeLongest = Math.max(subtreeLongest, right + 1);
        }
        longest = Math.max(subtreeLongest, longest);
        return subtreeLongest;
    }
}
```

Reference:

http://www.lintcode.com/en/problem/binary-tree-longest-consecutive-sequence/

http://www.jiuzhang.com/solutions/binary-tree-longest-consecutive-sequence/