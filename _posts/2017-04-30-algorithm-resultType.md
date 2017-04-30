---
layout: post
title: Jiuzhang-Result Type-Balanced binary tree
tags: algorithm jiuzhang binary_tree divide_conquer revisit resulttype
comments: true
---

>Q: Given a binary tree, determine if it is height-balanced. For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

Given a binary tree below, return false.
```
            1
              \
               10
              /  \
             4    7
```
This problem needs two pieces of information to make a decision: 
1. depth,
2. is balanced or not.

To find these two elements, we can use a **ResultType** class as a wrapper and simplify the problem.

```java
class ResulType{
    public boolean isBalanced;
    public int maxDepth;
    public ResultType(boolean isBalanced, int maxDepth){
        this.isBalanced = isBalanced;
        this.maxDepth = maxDepth;
    }
}

public class Solution {
    public boolean isBalanced(TreeNode root) {
        return helper(root).isBalanced;
    }
    public ResultType helper(TreeNode root){
        if (root == null){
            return new ResultType(true, 0);
        }
        //divide & conquer
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        //merge
        if (!left.isBalanced || !right.isBalanced){
            return new ResultType(false, -1);
        }
        if (Math.abs(left.maxDepth - right.maxDepth) > 1){
            return new ResultType(false, -1);
        }
        return new ResultType(true, Math.max(left.maxDepth, right.maxDepth) + 1);
    }
}
```
Jiuzhang has provided another way to solve the problem without ResulType.

```java
public class Solution {
    public boolean isBalanced(TreeNode root) {
        return maxDepth(root) != -1;
    }

    private int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        if (left == -1 || right == -1 || Math.abs(left-right) > 1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```

Reference:

http://www.lintcode.com/en/problem/balanced-binary-tree/