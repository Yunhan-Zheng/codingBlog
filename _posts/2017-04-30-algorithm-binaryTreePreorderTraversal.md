---
layout: post
title: Jiuzhang-Binary Tree Traversal--Preorder-Inorder-Postorder 
tags: algorithm jiuzhang binary_tree divide_conquer non-recursion revisit
date: 2017-04-30 10:05:14 -0400
comments: true
---

Q: Given a binary tree, find its preorder/inorder/postorder traversal.

    /**
    * Definition for binary tree
    * public class TreeNode {
    *     int val;
    *     TreeNode left;
    *     TreeNode right;
    *     TreeNode(int x) { val = x; }
    * }
    */

Example:

Given a binary tree, 
* to find its preorder, the result should be {1,2,10,4,7}; 
* to find its inorder, the result should be {2,1,4,10,7}; 
* to find its postorder, the result should be {2,4,7,10,1}.

```
            1
          /   \
         2    10
              /  \
             4    7
```

There are three ways to solve each order. 

### Preorder

```java
//Version 1. Non-recursive
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> preorder = new ArrayList<Integer>();
        if (root == null){
            return preorder;
        }
        stack.push(root);
        while (!stack.empty()){
            TreeNode node = stack.pop();
            preorder.add(node.val);
            if(node.right != null){
                stack.push(node.right);
            }
            if(node.left != null){
                stack.push(node.left);
            }
        }
        return preorder;
    }
}

//Version 2. Traverse
//Three steps to use recursion: define, break down, and exit.
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> preorder = new ArrayList<Integer>();
        helper(root, preorder);
        return preorder;
    }
    //define定义: put preorder of root into the result. 
    //与divide conquer不同的是通常返回值为void, 题目需要的result作为参数
    public void helper(TreeNode root, ArrayList<Integer> result){
        //exit 出口
        if (root == null){
            return;
        }
        //break down 拆解
        res.add(root);
        helper(root.left, result);
        helper(root.right, result);
    }
}

//Version 3. Divide & Conquer
public class Solution {
    //define: return preorder of root
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> preorder = new ArrayList<Integer>();
        //null or leaf
        if(root == null){
            return preorder;
        }
        //divide & conquer
        //任务的下派
        ArrayList<Integer> leftpath = preorderTraversal(root.left);
        ArrayList<Integer> rightpath = preorderTraversal(root.right);
        
        //merge
        //合并
        preorder.add(root.val);
        preorder.addAll(leftpath);
        preorder.addAll(rightpath);

        return preorder;
    } 
}
```

Traverse and Divide & Conquer work similarly for inorder and postorder compared with those for preorder. Here, I only list the non-recursive solutions provided by Jiuzhang.

### Inorder

```java
//Version 1. Non-recursive
public class Solution {
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> inorder = new ArrayList<Integer>();
        TreeNode curt = root;
        while (curt != null || !stack.empty()) {
            while (curt != null) {
                stack.add(curt);
                curt = curt.left;
            }
            curt = stack.pop();
            inorder.add(curt.val);
            curt = curt.right;
        }
        return inorder;
    }
}
```

### Postorder

```java
//Version 1. Non-recursive
public class Solution {
    public ArrayList<Integer> postorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode prev = null; // previously traversed node
        TreeNode curr = root;

        if (root == null) {
            return result;
        }

        stack.push(root);
        while (!stack.empty()) {
            curr = stack.peek();
            if (prev == null || prev.left == curr || prev.right == curr) { 
                // traverse down the tree
                if (curr.left != null) {
                    stack.push(curr.left);
                } else if (curr.right != null) {
                    stack.push(curr.right);
                }
            } else if (curr.left == prev) { // traverse up the tree from the left
                if (curr.right != null) {
                    stack.push(curr.right);
                }
            } else { // traverse up the tree from the right
                result.add(curr.val);
                stack.pop();
            }
            prev = curr;
        }

        return result;
    }
}
```

Reference:

[1] http://www.jiuzhang.com/solutions/binary-tree-preorder-traversal/

[2] http://www.jiuzhang.com/solutions/binary-tree-inorder-traversal/

[3] http://www.jiuzhang.com/solutions/binary-tree-postorder-traversal/