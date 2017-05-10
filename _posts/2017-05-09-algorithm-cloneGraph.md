---
layout: post
title: Jiuzhang-Clone Graph
tags: algorithm jiuzhang bfs revisit facebook
date: 2017-05-09 16:41:00 -0400
comments: true
---
<a href ="http://www.lintcode.com/en/problem/clone-graph/" target="_blank">Question Link</a>

To solve this problem, we can follow below three major steps:
 
1. find all nodes
2. clone nodes
3. clone edges

### Sample solution

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null){
            return node;
        }
        //find all nodes
        ArrayList<UndirectedGraphNode> nodes = getNodes(node);

        //copy nodes
        Map<UndirectedGraphNode, UndirectedGraphNode> mapping = new HashMap<>();
        for (UndirectedGraphNode n : nodes){
            mapping.put(n, new UndirectedGraphNode(n.label));
        }

        //copy edges
        for (UndirectedGraphNode n : nodes){
            UndirectedGraphNode newNode = mapping.get(n);
            for (UndirectedGraphNode neighbor : n.neighbors){
                mapping.get(n).neighbors.add(mapping.get(neighbor));
            }
        }
        return mapping.get(node);
    }
    private ArrayList<UndirectedGraphNode> getNodes(UndirectedGraphNode node){
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        Set<UndirectedGraphNode> hash = new HashSet<>();

        queue.offer(node);
        hash.add(node);
        while (!queue.isEmpty()){
            UndirectedGraphNode head = queue.poll();
            for (UndirectedGraphNode neighbor : head.neighbors){
                if (!hash.contains(neighbor)){
                    hash.add(neighbor);
                    queue.offer(neighbor);
                }
            }
        }
        return new ArrayList<UndirectedGraphNode>(hash);
    }
}
```

Reference:

http://www.jiuzhang.com/solutions/clone-graph/
