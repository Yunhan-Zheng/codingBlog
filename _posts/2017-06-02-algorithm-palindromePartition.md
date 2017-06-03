---
layout: post
title: Palindrome Partition
tags: algorithm jiuzhang backtracking dfs revisit
date: 2017-06-02 19:20:00 -0400
comments: true
---
<a href="http://www.lintcode.com/en/problem/palindrome-partitioning/" target="_blank">Palindrome Partition</a>

Example:

Given a string "aaa", return [["a","a","a"],["aa","a"],["aaa"]].

The following solution uses dynamic programming. 

```java
public class Solution {
    boolean[][] isPalindrome;
    List<List<String>> res;
    /**
     * @param s: A string
     * @return: A list of lists of string
     */
    public List<List<String>> partition(String s) {
        res = new ArrayList<>();
        if (s == null || s.length() == 0){
            return res;
        }
        
        getIsPalindrome(s);

        helper(s, 0, new ArrayList<Integer>());

        return res;
    }
    //DP
    private void getIsPalindrome(String s){
        int n = s.length();
        isPalindrome = new boolean[n][n];
        for (int i = 0; i < n; i++){
            isPalindrome[i][i] = true;
        }
        for (int i = 0; i < n - 1; i++){
            isPalindrome[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
        }
        for (int i = n - 3; i >= 0; i--){
            for (int j = i + 2; j < n; j++){
                isPalindrome[i][j] = isPalindrome[i + 1][j - 1] && (s.charAt(i) == s.charAt(j));
            }
        }
    }
    private void helper(String s, int start, List<Integer> partition){
        if (start == s.length()){
            addResult(s, partition);
            return;
        }
        for (int i = start; i < s.length(); i++){
            if (!isPalindrome[start][i]){
                continue;
            }
            partition.add(i);
            helper(s, i + 1, partition);
            partition.remove(partition.size() - 1);
        }
    }
    private void addResult(String s, List<Integer> partition){
        List<String> result = new ArrayList<>();
        int start = 0;
        for (int i = 0; i < partition.size(); i++){
            result.add(s.substring(start, partition.get(i) + 1));
            start = partition.get(i) + 1;
        }
        res.add(result);
    }
}
```

