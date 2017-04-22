---
layout: post
title: Permutation
tags: algorithm
comments: true
---

<a href="https://en.wikipedia.org/wiki/Permutation" target="_blank">Permutation</a> is a possible  ordered sequence of different elements. 

### Lexicographical order - permutation without recursion
> In mathematics, the lexicographic or lexicographical order (also known as lexical order, dictionary order, alphabetical order or lexicographic(al) product) is a generalization of the way the alphabetical order of words is based on the alphabetical order of their component letters. --Wiki

Suppose you have an array of three different elements `['a','b','c']`, the lexicographical ordering of these elements is **abc < acb < bac < bca < cab < cba**

Suppose P is a permutation of elements `[1,..,n]`, P=P<sub>1</sub>P<sub>2</sub>..P<sub>j</sub>P<sub>j+1</sub>..P<sub>k</sub>P<sub>k+1</sub>..P<sub>n</sub>. When searching from the right most of the array, I need to find the first element P<sub>j</sub> that allows P<sub>j</sub><P<sub>j+1</sub> and then find the first element P<sub>k</sub> that allows P<sub>k</sub>>P<sub>j</sub>. Swap P<sub>j</sub> with P<sub>k</sub>. Reverse the order of elements from index **j+1** to **n**. 

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
Given a charArray `abc`, all the permutations are `abc`,`bac`,`cba`,`acb`,`bca` and `cab`. In this permutation with recursion method, think `bac` and `cba` as results from swapping the first letter `a` with post letters `b` and `c` in `abc` respectively, while `acb` as a result from swapping `b` with its post letter `c` in `abc`. In general, permutation is equal to swapping a letter with other letters following it, starting from the first letter to the second last one.

```java
public static void main(String[] args){
    String str="abc";
    permutations(str,0,str.length);
}

//permutation with recursion. 'start' is the index of the starting point for swap;'len' is the length of the string.
private static void permutations(String str,int start, int len){
    if (start == len-1){
        println(str);
    }
    else{
        for(int i=start;i<len;i++){
            swap(str.charAt(start),str.charAt(i));
            permutations(str,start+1,len);
            swap(str.charAt(start),str.charAt(i));
        }
    }
}
//swap two letters
private static void swap(char a, char b){
    char tmp=a;
    a=b;
    b=tmp;
}
```

There is another permutation without recursion <a href="http://stackoverflow.com/a/11471673/6181661" target="_blank">solution</a> which I haven't figured it out. Any comments to help me out is welcome!

```java
private static void printPermutations(String str){
    int [] factorials = new int[str.length()+1];
    factorials[0] = 1;
    //generate the factorial
    for(int i=1; i<str.length();i++){
        factorials[i]=factorials[i-1]*i;
    }
    //permutating 
    for (int i=0; i<factorials[str.length()];i++){
        for (int j=0; j<str.length();j++){
            if(str.charAt(j)>str.charAt(j+1))
        }
    }
```

Reference: 

[1]-[permutationLex](http://introcs.cs.princeton.edu/java/23recursion/PermutationsLex.java.html)