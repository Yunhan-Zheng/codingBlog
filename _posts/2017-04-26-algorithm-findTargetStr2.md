---
layout: post
title: Leetcode-Find target string II
tags: algorithm leetcode easy jiuzhang
comments: true
---

Q: Same requirements as [Find target string]({{site.baseurl}}/2017/04/20/algorithm-findTargetStr.html) except the time complexity should be O(n+m) where the length of `source` is n and the length of `target` is m.  

This is implemented through Rabin–Karp algorithm, introduced in the post [Hash function]({{site.baseurl}}/2017/04/25/algorithm-hashFunction.html).

The sample solution is as follows.

```java
class Solution {
    public int strStr2(String source, String target) {
        int HASH_SIZE = 1000000;
        if(source == null || target == null){
            return -1;
        }
        int l = target.length();
        if(l == 0){
            return 0;
        }

        //31^l
        int power = 1;
        for (int i = 0; i < l; i++){
            power = (power * 31) % HASH_SIZE;
        }

        int targetcode = 0;
        for (int i = 0; i < l; i++){
            targetcode = (targetcode * 31 + target.charAt(i)) % HASH_SIZE
        }

        //hashcode source substring
        for(int i = 0; i < source.length(); i++){
            hashcode = (hashcode * 31 + source.charAt(i)) % HASH_SIZE;
            
            if(i < l - 1){
                continue;
            }
            
            //hashcode[bcd] = hashcode[abcd] - hashcode[a]
            if(i >= l){
                hashcode = hashcode - (source.charAt(i - l) * power) % HASH_SIZE;
                if(hashcode < 0){
                hashcode += HASH_SIZE;
                }
            }
            
            if (hashcode == targetcode){
                if(source.substring(i - l + 1, i + 1).equals(target)){
                    return i - l + 1;
                }
            }
        }
        return -1;
    }
};
```
