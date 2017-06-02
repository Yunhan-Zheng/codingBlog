---
layout: post
title: Number of Islands
tags: algorithm jiuzhang bfs revisit google facebook
date: 2017-05-13 12:44:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/number-of-islands/" target="_blank">Number of Islands</a>

### Sample solution

```java
class Coordinate {
    int x, y;
    public Coordinate(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
public class Solution {
    public int numIslands(boolean[][] grid) {
        int counter = 0;
        if (grid == null || grid.length == 0 || grid[0].length == 0){
            return counter;
        }
        int m = grid.length;
        int n = grid[0].length;
        
        for (int i = 0; i < m; i++){
            for (int j = 0; j < n; j++){
                if (grid[i][j]){
                    markByBFS(grid, i, j);
                    counter++;
                }
            }
        }
        return counter;
    }
    private void markByBFS(boolean[][] grid, int x, int y){
        int[] directionX = {1,-1,0,0};
        int[] directionY = {0,0,1,-1};

        Queue<Coordinate> queue = new LinkedList<>();
        queue.offer(new Coordinate(x, y));
        grid[x][y] = false;

        while (!queue.isEmpty()){
            Coordinate cur = queue.poll();
            for (int i = 0; i < 4; i++){
                Coordinate adj = new Coordinate(
                    cur.x + directionX[i], cur.y + directionY[i]);
                if (!inBound(grid, adj)){
                    continue;
                }
                if (grid[adj.x][adj.y]){
                    queue.offer(adj);
                    grid[adj.x][adj.y] = false;
                }
            }
        }
    }
    private boolean inBound(boolean[][] grid, Coordinate co){
        int m = grid.length;
        int n = grid[0].length;
        return co.x >= 0 && co.x < m && co.y >= 0 && co.y < n;
    }
}
```
Reference:

http://www.jiuzhang.com/solutions/number-of-islands/
