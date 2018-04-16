Factorial Trailing Zeroes
===

1.问题描述
---

Given an integer n, return the number of trailing zeroes in n!<br>
给定一个整数，返回n!末尾0的个数。

2.思路
---

由题意可知，5!有一个0，10!有两个0，15!有三个0，以此类推，可以用递归来解决这道题目。其实不难发现要想从一个0到第二个0，至少要乘以5.

3.代码I（递归）
---

```c
int trailingZeroes(int n) {
    return n == 0 ? 0 : n / 5 + trailingZeroes(n / 5);
}
```

4.代码II（循环）
---

```c
int trailingZeroes(int n) {
    int sum=0;
    while(n){
        sum+=n/5;
        n/=5;
    }
    return sum;
}
```

4.总结
---

不能只单纯地根据题目中的叙述来确定代码的过程，而是应该找到真正解决这道题的方法，比如这道题目，并没有真实地求出n!,而是通过0生成的过程来解决。
