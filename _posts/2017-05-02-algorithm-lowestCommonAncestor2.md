---
layout: post
title: Jiuzhang-Lowest Common Ancestor II & III
tags: algorithm jiuzhang binary_tree divide_conquer revisit resulttype
date: 2017-05-02 20:05:00 -0400
comments: true
---

### Lowest Common Ancestor II

>Q: Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes. The node is of the below class and has an attribute parent which point to the father of itself. The root's parent is null.

``` 
class ParentTreeNode {
     public ParentTreeNode parent, left, right;
}
```
Example:

Given a binary tree below, LCA(4, 13) = 13, and LCA(7, -2) = -1.
```
            -1
            /  \
           7   13
              /  \
             4    -2
```


Since there is no method to get the value of each node itself, we have to record its path to the root, if any. Then compare between the two paths.

```java
public class Solution {
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root,
                                                 ParentTreeNode A,
                                                 ParentTreeNode B) {
        ArrayList<ParentTreeNode> pathA = getPath(A);
        ArrayList<ParentTreeNode> pathB = getPath(B);

        ParentTreeNode lowestCommonAncestor = null;
        int indexA = pathA.size() - 1;
        int indexB = pathB.size() - 1;
        while (indexA >= 0 && indexB >= 0){
            if (pathA.get(indexA) != pathB.get(indexB)){
                break;
            }
            lowestCommonAncestor = pathA.get(indexA);
            indexA--;
            indexB--;
        }
        return lowestCommonAncestor;    
    }
    private ArrayList<ParentTreeNode> getPath(ParentTreeNode node){
        ArrayList<ParentTreeNode> path = new ArrayList<ParentTreeNode>();
        while (node != null){
            path.add(node);
            node = node.parent;
        }
        return path;
    }
}
```

### Lowest Common Ancestor III

Same question with <a href="{{site.baseurl}}/2017/05/01/lowestCommonAncestor.html" target="_blank">LCA</a> except nodes to find may not exist in the tree.

Since nodes may not exist, we need a flag to store the existence info. We then create a resultType in this solution. The ResultType class instance indicates that whether `A` and `B` exist in a tree with root `node`.

There are four scenarios in this problem:

1. A == root || B == root
2. left subtree contains one node && right subtree contains one node
3. only left subtree contains one node
4. only right subtree contains one node

```java
class ResultType {
    public boolean a_exist, b_exist;
    public TreeNode node;
    ResultType(boolean a, boolean b, TreeNode n) {
        a_exist = a;
        b_exist = b;
        node = n;
    }
}
public class Solution {
    public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode A, TreeNode B) {
        ResultType rt = helper(root, A, B);
        if (rt.a_exist && rt.b_exist)
            return rt.node;
        else
            return null;
    }
    public ResultType helper(TreeNode root, TreeNode A, TreeNode B){
        if (root == null){
            return new ResultType(false, false, null);
        }
        ResultType left_rt = helper(root.left, A, B);
        ResultType right_rt = helper(root.right, A, B);
        boolean a_exist = left_rt.a_exist || right_rt.a_exist || root == A;
        boolean b_exist = left_rt.b_exist || right_rt.b_exist || root == B;

        if (root == A || root == B){
            return new ResultType(a_exist, b_exist, root);
        }
        if (left_rt.node != null && right_rt.node != null){
            return new ResultType(a_exist, b_exist, root);
        }
        if (left_rt.node != null){
            return new ResultType(a_exist, b_exist, left_rt.node);
        }
        if (right_rt.node != null){
            return new ResultType(a_exist, b_exist, right_rt.node);
        }
        return new ResultType(false, false, null);
    }
```

Reference:

http://www.lintcode.com/en/problem/lowest-common-ancestor-ii/

http://www.lintcode.com/en/problem/lowest-common-ancestor-iii/