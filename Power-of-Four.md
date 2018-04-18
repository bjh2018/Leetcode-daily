Power of Four
===

1.问题描述
---

Given an integer (signed 32 bits), write a function to check whether it is a power of 4.<br> 
Example:<br>
Given num = 16, return true. Given num = 5, return false.<br>
给定一个32位的整型的数，判断它是不是4的幂。

2.思路
---

用一个循环来实现，如果该数除以4的余数为0的话，就把它除以4，以此类推，最后判断结果是否为0.

3.代码I
---

```c
bool isPowerOfFour(int num) {
    while (num>1) {
            if(num%4==0) {
                num=num/4;
            }
            else break;
        }
        return num==1;
}
```

4.代码II
---

```c
bool isPowerOfFour(int num) {
    if(num <= 0){
        return false;
    }
    return ( (num & (num - 1)) == 0) && ( (num & 0x55555555) != 0 );
}
```

0x55555555是16进制，2进制是1010101010101010101010101010101<br>
[思路来源](https://blog.csdn.net/qq_31597573/article/details/51181363)
