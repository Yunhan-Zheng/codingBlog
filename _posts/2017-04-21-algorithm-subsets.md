---
layout: post
title: Leetcode-Subsets I
tags: algorithm leetcode array bit_manipulation
comments: true
---

Q: Given a distinct array of integers `S`, return all subsets which are in non-descending order.

Example: input `{1,3,2}`, should return `{}`,`{1}`,`{2}`,`{3}`,`{1,2}`,`{1,3}`,`{2,3}` and `{1,2,3}`.

Thoughts:
1. Arrays.sort() can take care of non-descending order.
2. In a subset, elements can be picked or not picked using 0 or 1 as an indicator. Tha mapping for above example is as follows.

|bits|subset|
|:----:|:-------:|
|000 |{}|
|001 |{1}|
|010 |{2}|
|011 |{1,2}|
|100 |{3}|
|101 |{1,3}|
|110 |{2,3}|
|111 |{1,2,3}|

In below piece of code, it uses bit operation, which I have researched and summarized in another post, [Bit hacks]({{site.baseurl}}/2017/04/22/lowlevel-bitHacks.html).<sup>[1]</sup>

```java
class Solution {
  public ArrayList<ArrayList<Integer>> subsets(int[] S) {
    ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
    
    if(S == null || S.length == 0){

      Arrays.sort(S);

      int l = S.length;
        
      //there are 2^l subsets, type long limits l to 64
      long n = (long) Math.pow(2,l);

      for(int i = 0; i < n; i++){
        ArrayList<Integer> subset = new ArrayList<Integer>();
        long temp = i;
        while(temp != 0){
          int bitIndex = findLowestBit(temp);
          subset.add(S[bitIndex]);
          //clear processed bit
          temp ^= 1 << bitIndex;
        }
        result.add(subset);
      }
      return result;
    }
    else {
      return result;
    }
  }
  private static int findLowestBit(long value){
    return Long.numberOfTrailingZeros(value);
  }
}
```

If not solving this problem with bit operation, it's natural to consider the recursive algorithm. It uses depth-first searching for traversing or searching tree or graph data structures.<sup>[2]</sup>
```java
class Solution {
  public static ArrayList<ArrayList<Integer>> subsets(int[] S) {
        ArrayList<ArrayList<Integer>> ret = new ArrayList<ArrayList<Integer>>();
        if (S == null || S.length == 0) {
            return ret;
        }

        Arrays.sort(S);

        dfs(S, 0, new ArrayList<Integer> (), ret);

        return ret;
    }
    
    public static void dfs(int[] S, int index, ArrayList<Integer> path, ArrayList<ArrayList<Integer>> ret) {
        ret.add(new ArrayList<Integer>(path));

        for (int i = index; i < S.length; i++) {
            path.add(S[i]);
            dfs(S, i + 1, path, ret);
            path.remove(path.size() - 1); //backtrack to a node 
        }
    }
}
```

Reference: 

[1] :<a href='http://www.fusu.us/2013/07/the-subsets-problem.html' target='_blank'>http://www.fusu.us/2013/07/the-subsets-problem.html</a>

[2] :<a href='http://www.fusu.us/2013/07/the-subsets-problem.html' target='_blank'>https://en.wikipedia.org/wiki/Depth-first_search</a>