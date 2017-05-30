---
layout: post
title: Breadth First Search
tags: algorithm jiuzhang bfs revisit
date: 2017-05-05 14:01:00 -0400
comments: true
---
>Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph) and explores the neighbor nodes first, before moving to the next level neighbors. -- Wiki

Problems about below topics always will use BFS. BFS uses the **Queue** data structure very often.

* Traversal in graph
    * Level order traversal
    * Connected component
    * Topological sorting
* Shortest path in a simple graph

Let me take the level order traversal as an example. In a tree, we can use BFS to traverse the tree nodes from left to right, level by level.

Example:
{% raw %}
Given a below binary tree, return `{{3}, {9,20},{15,7}}`.
{% endraw %}

        3
       / \
      9  20
        /  \
       15   7

### Sample solution

```java
public class Solution {
    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if (root == null){
            return res;
        }
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(root);
        while (!q.isEmpty()){
            ArrayList<Integer> level = new ArrayList<>();
            int size = q.size();
            for (int i = 0; i < size; i++){
                TreeNode head = q.poll();
                level.add(head.val);
                if (head.left != null){
                    q.offer(head.left);
                }
                if (head.right != null){
                    q.offer(head.right);
                }
            }
            res.add(level);
        }
        return res;
    }
}
```

Reference:

https://en.wikipedia.org/wiki/Breadth-first_search

http://www.geeksforgeeks.org/applications-of-breadth-first-traversal/