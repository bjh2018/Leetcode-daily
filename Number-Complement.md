Number Complement
===

1.问题描述
---

Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.<br>
Note:<br>
The given integer is guaranteed to fit within the range of a 32-bit signed integer.<br>
You could assume no leading zero bit in the integer’s binary representation.<br>
<br>
Example 1:<br>
Input: 5<br>
Output: 2<br>
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.<br>
<br>
Example 2:<br>
Input: 1<br>
Output: 0<br>
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.<br>
给定一个正整数，输出其补数。 补充策略是翻转其二进制表示的位。

2.思路
---

把给出的数的二进制的各位都算出来，反转之后计算出反转之后的整数即可，可以用一个i来记录要乘的2的幂次。

3.代码I
---

```c
int findComplement(int num) {
    int i=1,b=1,sum=0;
    while (num>0) {
        b=num%2;
        if (b==1) b=0;
        else b=1;
        b=b*i;
        i=i*2;
        sum=sum+b;
        num=num/2;
    }
    return sum;
}
```

4.代码II
---

```c
int findComplement(int num) {
    long i;
    for(i=1;i<=num;i*=2) num^=i; 
    return num;

}
```

Entered: 4=>100;<br>
100 ^ 001 = 101;<br>
101 ^ 010 = 111;<br>
111 ^ 100 = 011;<br>
Out:     011=>3;<br>
