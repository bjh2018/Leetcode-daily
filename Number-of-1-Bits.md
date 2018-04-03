Number of 1 Bits
===

1.问题描述
---

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).<br>
For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.<br>
编写一个带有无符号整数的函数，并返回其具有的'1'位数（也称为汉明权重）。<br>
例如，32位整数'11'具有二进制表示00000000000000000000000000001011，所以函数应该返回3。<br>

2.思路
---

想到以前有一个题也是求一的个数，先把该数左移再右移，如果两数相等，那么说明该数的最后一位为0，然后把该数右移一位，再这样判断。But这道题是给了一个32位的整数，这样
就不能按这样的方法了。但是可以用与运算来实现，把给定的数与1进行与运算，如果结果不为0，则说明该数的最后一位为0，街巷来把该数再右移一位再判断即可。

3.代码
---

```c
int hammingWeight(uint32_t n) {
    int ret = 0;
    while (n) {
        if (n & 1)
            ret++;
        n >>= 1;
    }
    return ret;
}
```

4.代码II
---

```c
int hammingWeight(uint32_t n) {
    int cnt=0;
    while(n){
        n=n&(n-1);
        cnt++;
    }
    return cnt;
}
```

[n&(n-1)妙用](https://blog.csdn.net/u012965373/article/details/50592727)
