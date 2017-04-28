---
layout: post
title: Jiuzhang-Divide two integers
tags: algorithm binary_search jiuzhang
comments: true
---

Q: Divide two integers without using **multiplication**, **division** and **mod** operator. If it is overflow, return 2147483647. If it's underflow, return -2147483647. 

### Thoughts

Special situations to be considered first:

* divisor is 0;
* dividend is 0; 
* dividend is overflow or underflow when divisor is 1.

Then to speed up the deduction of divisor from dividend, use bit operator `<<` to increase divisor by a factor of 10<sup>n</sup> .

### sample solution

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        
        if(divisor == 0) {
            return dividend > 0? Integer.MAX_VALUE: Integer.MIN_VALUE;
        }
        else if(dividend == 0){
            return 0;
        }
        else if((long) dividend >= Integer.MAX_VALUE && Math.abs(divisor) == 1){
            return divisor > 0? Integer.MAX_VALUE: Integer.MIN_VALUE;
        }
        else if((long) dividend <= Integer.MIN_VALUE && Math.abs(divisor) == 1){
            return divisor < 0? Integer.MAX_VALUE: Integer.MIN_VALUE;
        }
        else {
            int quotient = 0;
            boolean isNegative = (dividend < 0 && divisor > 0) || 
                                (dividend > 0 && divisor < 0);
            long dd = Math.abs((long) dividend);
            long ds = Math.abs((long) divisor);
            while (dd >= ds){
               int shift = 0;
               while (dd >= (ds << shift)){
                   shift++;
               }
               dd -= ds << (shift - 1);
               quotient += 1 << (shift - 1);
            }
        
        return isNegative? -quotient: quotient;
        }
    }
}
```
Reference:

http://www.jiuzhang.com/solutions/divide-two-integers/