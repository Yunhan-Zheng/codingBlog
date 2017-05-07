---
layout: post
title: Jiuzhang-Combination Sum
tags: algorithm jiuzhang array sort backtracking dfs revisit
date: 2017-05-06 16:03:00 -0400
comments: true
---
>Q: Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same number may be chosen from C **unlimited** times.

Note:

* All numbers (including target) will be **positive** integers.
* Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
* The solution set must not contain duplicate combinations.

Example:

Given candidate set [2,3,5,8] and target 8, a solution set is:
    [8]
    [3,5]
    [2,3,3]

### Sample Solution

```java
public class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        if (candidates == null || candidates.length == 0){
            return res;
        }
        Arrays.sort(candidates);
        List<Integer> comb = new ArrayList<>();
        helper(candidates, 0, target, comb, res);
        return res;
    }
    private void helper(int[] candidates, int index, int target, List<Integer> comb, List<List<Integer>> res){
        if (target == 0){
            res.add(new ArrayList<Integer>(comb));
            return;
        }
        for (int i = index; i < candidates.length; i++){
            if (candidates[i] > target){
                break;
            }
            if (i != index && candidates[i] == candidates[i - 1]){
                continue;
            }
            comb.add(candidates[i]);
            helper(candidates, i, target - candidates[i], comb, res);
            comb.remove(comb.size() - 1);
        }
    }
}
```

Reference:

http://www.lintcode.com/en/problem/combination-sum/
