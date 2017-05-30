---
layout: post
title: Subsets II
tags: algorithm jiuzhang array recursion
comments: true
---

Q: Given a collection of integers that might contain duplicates, `S`, return all possible subsets with no duplication. Note: Elements in a subset must be in non-descending order. For example, If `S` = `{1,2,2}`, a solution is: `{ {}, {1}, {1,2}, {1,2,2}, {2}, {2,2} }`

Thoughts: Referring to the [subsets I]({{site.baseurl}}/2017/04/21/algorithm-subsets.html) problem, and use `{1,2',2"}` to apply the same code. Theoretically, the results will be `{ {}, {1}, {1,2'}, {1,2',2"}, {1,2"}, {2'}, {2',2"}, {2"} }`. Notice that if we prefer `2'` over `2"`, subsets `{1,2"}` and `{2"}` will be removed from the solution. What in common of these two is `2"` is picked while `2'` could have been picked but it is not. Therefore, the difference of this subset II problem is to add additional condition to `continue` the for loop.

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
          if(i != 0 && S[i] == S[i-1] && i > index){ //i != index ==> path.add(S[i-1]) is not executed + i always >= index ==> i > index
            continue;
          }
            path.add(S[i]);
            dfs(S, i + 1, path, ret);
            path.remove(path.size() - 1); 
        }
    }
}
```
