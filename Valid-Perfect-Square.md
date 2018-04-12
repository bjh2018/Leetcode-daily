 Valid Perfect Square
 ===
 
 1.问题描述
 ---
 
 Given a positive integer num, write a function which returns True if num is a perfect square else False.<br>
Note: Do not use any built-in library function such as sqrt. <br>
Example 1: <br>
Input: 16<br>
Returns: True<br>
<br>
Example 2:<br> 
Input: 14<br>
Returns: False<br>
给定一个整数，判断它是不是一个整数的幂。要求不能用库里的函数，比如sqrt函数。

2.思路
---

由题意可知，如果存在这样的整数，那么这样的整数一定小于等于num/2+1，所以就从1开始，来判断该数的平方与num的关系，如果相等，就返回true。

3.代码I
---

```c
bool isPerfectSquare(int num) {
    //return (sqrt(num)==(int)sqrt(num));
    for (int i=1; i<=num/2+1; i++) {
        if (i*i==num) return true;
    }
   return false;
}
```

[其他思路](https://blog.csdn.net/xiexingshishu/article/details/51782062)
