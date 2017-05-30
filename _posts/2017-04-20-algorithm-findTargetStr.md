---
layout: post
title: Find target string
tags: algorithm leetcode easy
comments: true
---

Q: Returns an index (0-based) of the first occurrence of target in source, or `-1` if target is not part of source.

Example: input `absncsn`,`sn`, should return `2`.

`source` string to be scanned.`target` string containing the sequence of characters to match.

```java
class Solution {
    public int strStr(String source, String target) {

        int index = -1;
        
        if(target == null || source == null){
            return index;
        }
        //return 0 if target is an empty string
        else if (target.equals("")){
            return 0;
        }
        else{
        //In this case, both source and target are not null.
        //loop though source to find the first letter of target until 
        //1)the rest of source cannot hold whole target
        //2)loop reaches the end letter of target

            int sl = source.length();
            int tl = target.length();
            for (int i =0; i < sl; i++){
              if(source.charAt(i) == target.charAt(0)){

                boolean existed = true;
                    
                for(int j = 1; j < tl; j++){
                  if((i + j) >= sl || source.charAt(i + j) != target.charAt(j)){
                    existed = false;
                  }
                }
                
                if(existed){
                  index = i;
                  break;
                }
              }
            }
        }
        return index;
    }
}
```