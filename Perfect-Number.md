Perfect Number
===

1.问题描述
---

We define the Perfect Number is a positive integer that is equal to the sum of all its positive divisors except itself. <br>
Now, given an integer n, write a function that returns true when it is a perfect number and false when it is not. <br>
<br>
Example:<br>
Input: 28<br>
Output: True<br>
Explanation: 28 = 1 + 2 + 4 + 7 + 14<br>
我们定义完美数是一个正整数，它等于除它自身之外的所有正因子的总和。现在，给定一个整数n，编写一个函数，当它是一个完美数字时返回true，否则返回false。

2.思路
---

首先就要找到给定整数的所有正因子，可以从2开始用循环来解决，要注意的是正因子最大不会超过n/2，所以在写的时候要注意范围。还要注意，1不符合条件。

3.代码
---

```c
bool checkPerfectNumber(int num) {
    int ans=1;
    for (int i=2; i<=num/2; i++) {
        if (num%i==0) ans+=i;
    }
    if (num==ans&&num!=1) return true;
    else return false;
}
```

4.其他代码
---

```c
bool checkPerfectNumber(int num) {
    int i,ans=1;
    if(num==1) return false;
    if(num==2) return false;
    if(num==3) return false;
    for(i=2; i<sqrt(num);i++)
    {
        if(num%i==0)
            ans +=(i+num/i);
    }
    

    
    return ans==num;
}
```

根据题意直推代码，初始化sum = 1，从2到sqrt(num)遍历当前数是否是num的因子，是的话加上i和num/i.
