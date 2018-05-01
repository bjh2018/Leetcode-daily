Binary Number with Alternating Bits
===

1.问题描述
---

Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.<br>
Example 1:<br>
Input: 5<br>
Output: True
Explanation:<br>
The binary representation of 5 is: 101<br>
<br>
Example 2:<br>
Input: 7<br>
Output: False<br>
Explanation:<br>
The binary representation of 7 is: 111.<br>
<br>
Example 3:<br>
Input: 11<br>
Output: False<br>
Explanation:<br>
The binary representation of 11 is: 1011.<br>
<br>
Example 4:<br>
Input: 10<br>
Output: True<br>
Explanation:<br>
The binary representation of 10 is: 1010.<br>
给定一个正整数，检查它是否有交替位：即，如果两个相邻位总是有不同的值。

2.思路
---

用两个整型的数来记录当前的一位的数，然后把数向右移一位，然后再记录最后一位的数，如果和上一个数相同，就返回false，如果不相等，就接着循环，知道n变为0.

3.代码
---
```c
bool hasAlternatingBits(int n) {
    int a=0,b=0;
    while (n) {
        a=n%2;
        n=n>>1;
        b=n%2;
        if (a==b)
            return false;
    }
    return true;
}
```
4.代码II
```c
bool hasAlternatingBits(int n) {
    
    int temp = n;
    int tag; 
    if((n>>1)<<1 != n)
        tag = 1;
    else 
        tag = 0;
    n>>=1;
    
    while(n)
    {
        if( (n>>1)<<1 != n)//代表当前为是1
        {
            if(tag==1)//代表附近两位相同
                return false;
            tag = 1;
        }
        else//当前位是0
        {
            if(tag==0)//代表附近两位相同
                return false;
            tag = 0;
        }
        n>>=1;
    }
    return true;
}
```
