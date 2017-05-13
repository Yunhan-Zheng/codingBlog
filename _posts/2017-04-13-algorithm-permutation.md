---
layout: post
title: Permutation
tags: algorithm jiuzhang dfs
comments: true
---

<a href="https://en.wikipedia.org/wiki/Permutation" target="_blank">Permutation</a> is a possible  ordered sequence of elements. 

### Lexicographical order - permutation without recursion
> In mathematics, the lexicographic or lexicographical order (also known as lexical order, dictionary order, alphabetical order or lexicographic(al) product) is a generalization of the way the alphabetical order of words is based on the alphabetical order of their component letters. --Wiki

Suppose you have an array of three elements `['a','b','c']`, the lexicographical ordering of these elements is **abc < acb < bac < bca < cab < cba**.

How it works to generate lexicographical ordering?

Suppose P is a permutation of elements `[P1,..,Pn]`. P=P<sub>1</sub> P<sub>2</sub> .. P<sub>j</sub> P<sub>j+1</sub> .. P<sub>k</sub> P<sub>k+1</sub> .. P<sub>n</sub>. When searching from the right most of the array, we need to find the first element P<sub>j</sub> that allows P<sub>j</sub> < P<sub>j+1</sub> and then find the first element P<sub>k</sub> that allows P<sub>k</sub> > P<sub>j</sub>. Swap P<sub>j</sub> with P<sub>k</sub>. Reverse the order of elements from index **j+1** to **n**. 

Therefore, the code to generate all permutations based on lexicographical order in Java is as follows.<sup>[1]</sup> 

```java
import java.util.Arrays;

public class permutateCharArray {
    public static void main(String[] args){
        char[] cStr={'b','a','a'};
        //sort array into an ascending order
        Arrays.sort(cStr);
        
        int n=cStr.length;

        perm(cStr);

    }
    private static void perm(char[] chars){
        if(chars.length==1){
            System.out.println(chars);
        }

        //print permutation
        show(chars);
        
        while(hasNext(chars)){
            show(chars);
        }
    }

    private static void show(char[] chars){
        for(int i=0;i<chars.length;i++){
            System.out.printf("%s",chars[i]);
        }
        System.out.println();
    }

    private static boolean hasNext(char[] chars){
        int n=chars.length;
        int j,k=n-1;

        for (j=n-2;j>=0;j--){
            if (chars[j]<chars[j+1]) {
                break;
            }
        }
        if(j==-1){
            return false;
        }
        //if array does not have duplicates, chars[k]<chars[j]
        while (chars[k]<=chars[j]){ 
            k--;
        }
        swap(chars,j,k);
        //reverse charactors from index j+1
        for(int s=j+1,t=n-1;s<t;s++,t--){
            swap(chars,s,t);
        }
        return true;

    }

    //swap two letters in a charactor array
    private static void swap(char[] a, int i, int j){
        char tmp=a[i];
        a[i]=a[j];
        a[j]=tmp;
    }
}
```
### Permutation with recursion
1. Given an integer array with **no duplicates** `123`, all the permutations are `123`,`213`,`321`,`132`,`231` and `312`. We will use DFS to solve it.

```java
public class Solution {
    public List<List<Integer>> permute(int[] nums) {
         ArrayList<List<Integer>> rst = new ArrayList<List<Integer>>();
         if (nums == null) {
             return rst; 
         }
         
         if (nums.length == 0) {
            rst.add(new ArrayList<Integer>());
            return rst;
         }

         ArrayList<Integer> list = new ArrayList<Integer>();
         helper(rst, list, nums);
         return rst;
    }
    
    public void helper(ArrayList<List<Integer>> rst, ArrayList<Integer> list, int[] nums){
        if(list.size() == nums.length) {
            rst.add(new ArrayList<Integer>(list));
            return;
        }
        
        for(int i = 0; i < nums.length; i++){
            if(list.contains(nums[i])){
                continue;
            }
            list.add(nums[i]);
            helper(rst, list, nums);
            list.remove(list.size() - 1);
        }
    }
}
```
2. Given an integer array with **duplicates**, find all unique permutations.

Example:

Given `[1,2,2]`, return `[[1,2,2], [2,1,2], [2,2,1]]`. 

Thoughts:
To distinguish two 2s, we use 2' and 2''. We order that 2'' cannot appear before 2'. Therefore, in the recursion method, we need to use an array called visited to store that information.

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums == null){
            return res;
        }
        int l = nums.length;
        if (l == 0){
            res.add(new ArrayList<Integer>());
            return res;
        }
        Arrays.sort(nums);
        ArrayList<Integer> list = new ArrayList<>();
        int[] visited = new int[l];
        for (int i = 0; i < l; i++){
            visited[i] = 0;
        }
        helper(res, list, visited, nums);
        return res;
    }
    private void helper(List<List<Integer>> res, ArrayList<Integer> list, int[] visited, int[] nums){
        if (list.size() == nums.length){
            res.add(new ArrayList<Integer>(list));
            return;
        }
        for (int i = 0; i < nums.length; i++){
            if (visited[i] == 1 || (i != 0 && visited[i-1] == 0 && nums[i] == nums[i-1])){
                continue;
            }
            visited[i] = 1;
            list.add(nums[i]);
            helper(res, list, visited, nums);
            list.remove(list.size() - 1);
            visited[i] = 0;
        }
    }
}
```

There is another permutation without recursion <a href="http://stackoverflow.com/a/11471673/6181661" target="_blank">solution</a> which I haven't figured it out. Any comment to help me out is welcome!

```java
private static void printPermutations(String str){
    int [] factorials = new int[str.length() + 1];
    factorials[0] = 1;
    //(length-1)!
    for(int i = 1; i < str.length(); i++){
        factorials[i] = factorials[i-1] * i;
    }
    for (int i = 0; i < factorials[string.length()]; i++) {
            String onePermutation="";
            String temp = string;
            int positionCode = i;
            for (int position = string.length(); position > 0 ; position--){
                int selected = positionCode / factorials[position - 1];
                onePermutation += temp.charAt(selected);
                positionCode = positionCode % factorials[position - 1];
                temp = temp.substring(0, selected) + temp.substring(selected + 1);
            }
            System.out.println(onePermutation);
        }
}
```

Reference: 

[1]-[permutationLex](http://introcs.cs.princeton.edu/java/23recursion/PermutationsLex.java.html)