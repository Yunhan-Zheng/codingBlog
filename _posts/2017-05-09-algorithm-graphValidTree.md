---
layout: post
title: Jiuzhang-Graph Valid Tree
tags: algorithm jiuzhang union_find bfs revisit facebook
date: 2017-05-09 16:01:00 -0400
comments: true
---
>Q: Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree. Assume that no duplicate edges. All edges are undirected, which means that [0, 1] is the same as [1, 0] and thus the two will not appear together in edges.

Example:

Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

For a tree, the number of edges is one less than the number of nodes and every node is connected to each other whether directly or indirectly.

In the given sample, we will use adjacency list to represent a graph. Graph can be represented by adjacency matrix. However, in code interviews, this data structure will sometimes be used for input parameter. It's not suggested to use adjacency matrix to solve a problem because its space complexity is n*n.

### Sample solution

```java
public class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (n <= 0){
            return false;
        }
        if (edges == null || edges.length != n - 1){
            return false;
        }
        Map<Integer, Set<Integer>> graph = initializeGraph(n, edges);

        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> hash = new HashSet<>();

        queue.offer(0);
        hash.add(0);
        while(!queue.isEmpty()){
            int node = queue.poll();
            for (Integer neighbor : graph.get(node)){
                if (hash.contains(neighbor)){
                    continue;
                }
                queue.offer(neighbor);
                hash.add(neighbor);
            }
        }
        return hash.size() == n;    
    }
    private Map<Integer, Set<Integer>> initializeGraph(int n, int[][] edges) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int i = 0; i < n; i++) {
            graph.put(i, new HashSet<Integer>());
        }

        //edges是二维数组，N行2列
        for (int i = 0; i < edges.length; i++) {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        return graph;
    }
}
```

Another solution uses Union Find which I'll update my thoughts later.

```java
public class Solution {
      class UnionFind{
        HashMap<Integer, Integer> father = new HashMap<Integer, Integer>();
        UnionFind(int n){
            for(int i = 0 ; i < n; i++) {
                father.put(i, i); 
            }
        }
        int compressed_find(int x){
            int parent =  father.get(x);
            while(parent!=father.get(parent)) {
                parent = father.get(parent);
            }
            int temp = -1;
            int fa = father.get(x);
            while(fa!=father.get(fa)) {
                temp = father.get(fa);
                father.put(fa, parent) ;
                fa = temp;
            }
            return parent;
                
        }
        
        void union(int x, int y){
            int fa_x = compressed_find(x);
            int fa_y = compressed_find(y);
            if(fa_x != fa_y)
                father.put(fa_x, fa_y);
        }
    }

    public boolean validTree(int n, int[][] edges) {
        // tree should have n nodes with n-1 edges
        if (n - 1 != edges.length) {
            return false;
        }
        
        UnionFind uf = new UnionFind(n);
        
        for (int i = 0; i < edges.length; i++) {
            if (uf.compressed_find(edges[i][0]) == uf.compressed_find(edges[i][1])) {
                return false;
            }
            uf.union(edges[i][0], edges[i][1]);
        }
        return true;
    }
}
```

Reference:

http://www.jiuzhang.com/solutions/graph-valid-tree/
