---
layout: post
title: Jiuzhang-Subtree with Maximum Average
tags: algorithm jiuzhang binary_tree divide_conquer revisit resulttype
date: 2017-04-30 19:05:38 -0400
comments: true
---

>Q: Given a binary tree, find the subtree with maximum average. Return the root of the subtree. Assume that there is only one subtree with maximum average.

Example:

Given a binary tree below, return 13.
```
            -1
              \
               13
              /  \
             4    -2
```
This problem needs two pieces of information to make a decision: 
1. subtree sum,
2. subtree size.

To find these two elements, we can again use the **ResultType** class as a wrapper.

```java
class ResultType{
    public int sum, size;
    public ResultType(int sum, int size){
        this.sum = sum;
        this.size = size;
    }
}

public class Solution {
    //全局变量
    private TreeNode subtree = null;
    private ResultType subtreeResult = null;

    public TreeNode findSubtree2(TreeNode root) {
        helper(root);
        return subtree;
    }
    private ResultType helper(TreeNode root){
        if (root == null){
            return new ResultType(0, 0);
        }
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        //当前根节点result merge
        ResultType result = new ResultType(
            left.sum + right.sum + root.val, 
            left.size + right.size + 1
            );
        //a / b > c / d => a * d > b * c, given bd > 0
        if (subtree == null || 
        subtreeResult.sum * result.size < subtreeResult.size * result.sum){
            subtree = root;
            subtreeResult = result;
        }
        return result;
    }
}
```

Reference:

http://www.lintcode.com/en/problem/subtree-with-maximum-average/