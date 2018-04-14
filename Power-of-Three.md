Power of Three
===

1.问题描述
---

Given an integer, write a function to determine if it is a power of three. <br>
给定一个整数，判断它是不是3的幂。

2.思路
---

一开始打算用一般的方法，从正向让给定的整数不断地除以3，最后愉快的超时了。但是如果从另一个方向看的话，可以用pow的函数来实现，因为给定的正整数，int型，有一定的范围，
可以让可能的最大的值对该数取余，如果余数为0，则说明给定的数是符合条件的。

3.代码
---

```c
bool isPowerOfThree(int n) {
    return (n > 0) && ((int)(pow(3, 19)) % n == 0);}
```

