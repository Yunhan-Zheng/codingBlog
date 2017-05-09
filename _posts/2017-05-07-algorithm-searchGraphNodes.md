---
layout: post
title: Jiuzhang-Search Graph Nodes
tags: algorithm jiuzhang array bfs revisit apple
date: 2017-05-07 18:01:00 -0400
comments: true
---
>Q: Given an undirected graph, a node and a target, return the node mapping to the target value nearest to the given node, return NULL if you can't find.

Note: it's guaranteed that there is only one available solution.

Example:

    2------3  5
     \     |  | 
      \    |  |
       \   |  |
        \  |  |
          1 --4

There a hash named values which is [3,4,10,50,50], representing:
Value of node 1 is 3
Value of node 2 is 4
Value of node 3 is 10
Value of node 4 is 50
Value of node 5 is 50

Give a node 1, target is 50, return node 4

### Sample solution

```java
/**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public class Solution {
    public UndirectedGraphNode searchNode(ArrayList<UndirectedGraphNode> graph,
                                          Map<UndirectedGraphNode, Integer> values,
                                          UndirectedGraphNode node,
                                          int target) {
        if (graph == null || graph.size() == 0){
            return null;
        }
        
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        Set<UndirectedGraphNode> hash = new HashSet<UndirectedGraphNode>();

        queue.offer(node);
        hash.add(node);

        while (!queue.isEmpty()){
            UndirectedGraphNode head = queue.poll();
            if (values.get(head) == target){
                return head;
            }
            for (UndirectedGraphNode n : head.neighbors){
                if (!hash.contains(n)){
                    queue.offer(n);
                    hash.add(n);
                }
            }
        }
        return null;
    }
}
```

Reference:

http://www.lintcode.com/en/problem/search-graph-nodes/
